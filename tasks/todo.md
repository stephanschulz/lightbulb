# A19 LED Filament Bulb — Interactive 3D Web App

## Goal
Build an interactive, adjustable 3D model of a polycarbonate A19 LED filament bulb
with 4 vertical filaments. The incline angle of the filaments is unknown, so make it
the primary adjustable parameter, alongside other real measured dimensions.

## Measured specs (from caliper photos in `source photos/`)
- Overall height incl. base: 102.05 mm
- Max glass diameter: 58.27 mm (spec "size 60")
- E26 cap diameter: 27.46 mm
- Filament length w/ contacts: 38.07 mm (spec "4*38mm")
- Filament glowing length: 30.16 mm
- Stem bottom → top of filament: 60.09 mm
- Stem bottom → bottom of filament glow: 25.18 mm
- 4 filaments, 2700K, 4W, 320lm, E26, 24V, dimmable, clear

## Plan
- [x] Extract measurements from photos
- [x] Scaffold single-file Three.js web app (CDN ESM + importmap)
- [x] Build A19 glass envelope via LatheGeometry (transmissive glass)
- [x] Build E26 metal base (threads, insulator, contact tip)
- [x] Build central glass stem + top/bottom support wires
- [x] Build 4 filaments with adjustable incline angle + bow
- [x] Warm emissive filaments + UnrealBloom glow + Kelvin→RGB color
- [x] OrbitControls + lil-gui adjustable panel (live regenerate)
- [x] Info overlay with specs; presets + reset
- [x] Local server + browser verification

## Review
- Single self-contained `index.html` (Three.js 0.160 ESM via CDN + lil-gui + UnrealBloom).
- A19 glass via LatheGeometry from a hand-tuned A19/A60 silhouette, transmissive
  MeshPhysicalMaterial with RoomEnvironment reflections.
- E26 base: brass screw shell + thread rings + white insulator + nickel tip + glass shoulder.
- Central glass stem + 4 filaments built as CatmullRom tubes with adjustable incline & bow,
  plus metal support wires top/bottom (matches the photos' cage shape).
- Glow: emissive filaments scaled by the dimmer, Kelvin→RGB color, point light, bloom.
- GUI live-regenerates geometry; presets (vertical/cage/splayed) + reset-to-measured.
- Incline angle is the headline control with a live bottom badge (the unknown spec).
- Verified: served via `python3 -m http.server`, node --check on the module passed,
  screenshot confirms correct render (glass, 4 glowing filaments, base, panels, badge).

## How to run
`cd` into project, `python3 -m http.server 8000`, open http://localhost:8000
