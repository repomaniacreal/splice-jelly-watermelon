# Melon Club — Slice Sprint

Melon Club is a browser-based 3D arcade game where players slice a watermelon jelly as many times as possible in a 15-second sprint. This recreation keeps the original game's core mechanics while introducing a new arcade-inspired interface with a plum background, coral accents, lime highlights, and a redesigned responsive layout.

## Features

- **3D slicing arena** powered by a bundled copy of Three.js.
- **15-second challenge** that starts with the first attempted cut.
- **Score tracking** with one point for every successful slice.
- **Animated slicing effects**, separated melon pieces, seeds, and particles.
- **Personal best** stored in the browser using `localStorage`.
- **Leaderboard interface** for viewing and submitting scores.
- **Responsive UI** for desktop and mobile screens.
- **Keyboard, mouse, and touch controls**.
- **Reduced-motion support** for users who prefer fewer animations.

## Project Files

```text
.
├── index.html   # Complete game: HTML, CSS, JavaScript, and bundled Three.js
└── README.md    # Project documentation
```

The game is intentionally packaged as a single HTML file. No package manager or build step is required.

## How to Run

### Option 1: Open the file

1. Download `index.html`.
2. Open it in a modern browser such as Chrome, Edge, Firefox, or Safari.
3. Make sure WebGL is enabled for the 3D scene.

### Option 2: Use a local development server

For a more consistent browser environment, serve the files locally. If Python 3 is installed, open a terminal in the project folder and run:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000> in your browser.

## How to Play

1. Aim the knife at the watermelon.
2. Make a cut. The 15-second timer starts with the first attempted cut.
3. Each successful slice earns one point.
4. Keep slicing until the timer reaches zero.
5. Enter a nickname to submit the result to the leaderboard, if the cloud service is available.
6. Select **Play Again** or use the restart control to begin another round.

## Controls

| Input | Action |
| --- | --- |
| Move the mouse or touch the arena | Aim the knife |
| Click or tap | Attempt a cut |
| Drag downward | Perform a slicing gesture |
| `←` / `→` | Move the aim position |
| `Space` | Attempt a cut |
| `R` | Restart the round |

On mobile devices, use touch gestures and the on-screen controls.

## Technology

- HTML5
- CSS3, including responsive media queries and reduced-motion preferences
- Vanilla JavaScript
- Three.js r160, bundled inside `index.html`
- Browser `localStorage` for the personal-best value and session data
- Supabase REST API and RPC calls for cloud leaderboard operations

## Leaderboard Configuration

The current implementation is wired to a Supabase project and expects these RPC functions to exist:

- `jelly15_leaderboard`
- `jelly15_submit_score`
- `jelly15_personal_best`

Anonymous authentication must also be enabled in the Supabase project. If the required backend functions or permissions are unavailable, cloud leaderboard and score-submission features may fail even though the local game can still be played.

For a different Supabase project, update the project URL and public client key in the `JellyCloud` configuration inside `index.html`, and make sure the backend RPC contracts match the requests made by the game. **Never put a Supabase service-role key in a client-side HTML file.** Public client keys are intended for browser use only when database access is correctly secured with server-side validation and appropriate Row Level Security policies.

## Browser Compatibility

Use a current browser with WebGL support. The 3D scene may not start if WebGL is disabled or unavailable. Internet access is required for Supabase-backed leaderboard features.

## Notes

- This project is a single-page browser game; it does not require Node.js to run.
- The personal-best value is stored per browser and device.
- Cloud leaderboard availability depends on the configured Supabase service and its database rules.
- The client performs basic score/rules checks, but trusted competitive scoring should always be validated on the server.
