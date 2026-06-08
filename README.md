# A19 LED Filament Bulb — Interactive 3D Model

An adjustable, explorable 3D rendering of the polycarbonate A19 LED filament bulb
(2700K · 4W · 320lm · E26 · 24V · clear · dimmable, 4×38mm filaments).

Built from the caliper measurements in `source photos/`.

## Run it

ES-module imports are blocked over `file://`, so serve it over a tiny local server:

```bash
cd "/Users/stephanschulz/Documents/cursor_ai/lightbulb"
python3 -m http.server 8000
```

Then open <http://localhost:8000> in a browser. (First load fetches Three.js +
lil-gui from a CDN, so you need internet the first time.)

## Controls

- **Drag** to orbit, **scroll** to zoom, **right-drag** to pan.
- Top-right panel adjusts every dimension live.
- **View** folder:
  - *Render mode*: **Technical (CAD)** — grey shaded surfaces + black feature edges,
    glass shown as a wireframe-of-revolution — or **Realistic** — transmissive glass
    with warm glow and bloom.
  - *Orthographic*: true engineering projection ⇄ free perspective orbit.
  - *Line weight* and *Surface shade* tune the drafting look.
  - *Dimensions*: overlay engineering dimension lines (extension lines, arrowheads,
    value labels) for overall height, max diameter, E26 cap, and filament length — the
    values update live as you change the parameters.
- **Filament incline angle** is the unknown spec — it's the headline control, with a
  live readout in the bottom badge. Presets: *Vertical*, *Cage (converging)*,
  *Splayed (flared)*.
- **Top twist °** pins each filament's bottom anchor and rotates only the top, twisting
  the cage into a helix.

All settings are **saved to browser memory** (`localStorage`) automatically and restored
on reload. *Reset to measured* clears them back to the measured defaults.

## Rendering

Three.js (r160) on the browser's WebGL rasterizer. Technical mode uses `LineSegments2`/
`Line2` fat lines for edges over flat-shaded surfaces (genuine hidden-line via the depth
buffer); realistic mode uses `MeshPhysicalMaterial` transmission + `UnrealBloom`.

## Measured dimensions used

| Measurement | Value |
|---|---|
| Overall height (incl. base) | 102.05 mm |
| Max glass diameter | 58.27 mm |
| E26 cap diameter | 27.46 mm |
| Filament length (with contacts) | 38.07 mm |
| Filament glow length | 30.16 mm |
| Stem bottom → top of filament | 60.09 mm |
| Stem bottom → bottom of glow | 25.18 mm |
| Filament count | 4 |

## Files
- `index.html` — the entire self-contained app (Three.js + post-processing bloom).
- `source photos/` — caliper measurement photos.
- `tasks/todo.md` — build plan & notes.
