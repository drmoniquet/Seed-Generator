# Seed Generator

A walkable 3D environment for the web: a dark, foggy space, a boardwalk over animated water, and two video screens hovering ahead at angles to each other, catching your approach from either side. Built with three.js, no build step — it runs by opening `index.html` in a browser (served, not double-clicked — see below).

## Adding your films

Drop your two exports into `videos/`, named:

```
videos/screen-a.mp4   ← left-hand screen
videos/screen-b.mp4   ← right-hand screen
```

That's the only thing that needs to match — the page finds them by filename automatically. If you'd rather keep your own filenames, change the two `src="videos/..."` paths on the `<video>` elements near the top of `index.html`.

Send me the two files and I'll drop them in and confirm here.

## Moving through the space

- **WASD** or **arrow keys** — walk
- **Mouse** — look around (the browser locks the pointer once you click "enter," so movement feels like a real walkthrough rather than a dragged orbit)
- **Esc** — release the pointer, back to the intro screen

Walking is soft-bounded to a wide circle around the scene, so a visitor can wander off the boardwalk into the water's edge without ever reaching a hard wall or the void beyond the fog.

## The one-page layout, roughly

- **Water** — a large plane, subdivided and animated with a gentle sine-wave displacement each frame, dark and faintly reflective.
- **Boardwalk** — individual plank meshes laid end to end, each nudged very slightly off-true so the path doesn't read as machine-perfect.
- **Two screens** — video-textured planes hovering above the water at the end of the path, each rotated away from the other (`screenAngle` in the config), so they present at a real angle rather than sitting parallel like a diptych. Each has a soft point light matched to a faint frame glow, so the screens feel like they're casting light into the fog rather than just floating flat.

## Tuning it

Everything you're likely to want to adjust lives in one `CONFIG` object near the top of the `<script type="module">` block in `index.html` — no need to hunt through the rest of the code:

| Setting | Controls |
|---|---|
| `fogDensity` | how quickly the space disappears into darkness with distance |
| `waveHeight`, `waveSpeed` | how restless the water looks |
| `pathLength` | how far the boardwalk runs before the screens |
| `screenDistance` | how far ahead the screens hover |
| `screenSpread` | how far apart the two screens sit, left/right |
| `screenAngle` | how sharply each screen turns away from the other — this is the "hovering at angles" geometry |
| `screenHeightAbove` | how high above the water the screens float |
| `walkSpeed` | visitor's walking pace |
| `boundsRadius` | how far a visitor can wander from centre before being gently held back |

## Running it locally

Video and module-script loading both require a real server, not a `file://` double-click. From inside this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Deploying to GitHub Pages

Same pattern as your other web pieces:

```bash
git init
git add .
git commit -m "Seed Generator"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then **Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main`, folder `/ (root)`. It'll publish at `https://<your-username>.github.io/<repo-name>/`.

**On file size:** mp4 exports for two full screens can get large fast. If GitHub's 100MB-per-file limit or the general repo-size guidance becomes a problem, the fix is the same as before — compress harder, or host the video files elsewhere (a CDN, a cloud bucket) and point the two `src="..."` paths at those URLs instead of a local file. Nothing else about the scene changes.

## For the CFP submission

If the journal wants something viewable without anyone needing to walk it themselves — a still, a short capture, or a fixed-camera version — say so and I can add a second camera mode (a slow scripted drift down the boardwalk toward the screens) that runs automatically, so reviewers get the space without needing WASD.
