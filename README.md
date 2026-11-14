# zijun198.github.io (gateway)

A small landing page that sends visitors to the main site, **https://pacguy-mtk.github.io/**.

- Shows two choices: **3D Room** (`room.html?mode=room`) and **Classic site** (`?mode=classic`).
- Auto-redirects after **10 seconds** to the highlighted choice. Visitors can click either card, press `R` / `C`, press `Enter` to go now, or `Esc` / the Pause button to stop the timer.
- Default choice: `?to=room|classic` in the URL, else the visitor's last choice (stored in `localStorage.zj_gate` on this domain), else the 3D Room. Visitors whose browser cannot run WebGL, bots and Data Saver users default to Classic (same checks as the main site).
- If the visitor returns with the Back button, the timer starts paused so they are not bounced again.
- No JavaScript: a `<noscript>` meta refresh opens the classic site after 10 seconds.

## Files
- `index.html`: the whole page (HTML, CSS, JS). Palette and fonts match the main site (Inter, #07111f, cyan #42e8d4, violet #8b5cf6, blue #7aa7ff).
- `assets/bg.mp4`: background video (H.264, 832 px wide, no audio, about 2.3 MB). Re-encoded from the original `202605171619.mp4` with the black bars cropped.
- `assets/bg-poster.jpg`: first-paint image shown while the video loads, or when motion is reduced.

## Common edits
- Timer length: `TOTAL_MS` in the script (currently `10000`).
- Destinations: `TARGETS` in the script, and the two `href`s on `.choice` links (kept in sync by the script, the HTML values are the no-JS fallback).
- Video: replace `assets/bg.mp4` (keep it under about 3 MB, muted, looping). Re-encode with:
  `ffmpeg -i input.mp4 -an -vf "scale=832:-2,fps=24" -c:v libx264 -crf 29 -pix_fmt yuv420p -movflags +faststart assets/bg.mp4`
