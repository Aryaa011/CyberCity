
 🤖 Cyber City Explorer

An interactive 3D browser experience where you control a robot exploring the **Overleague Cyber City** — a massive abandoned racing arena. Built entirely in a single HTML file with no server, no install, no dependencies.

---

## 🎮 Live Demo
https://cybercityexplorer.netlify.app

---

## ✨ Features

### Phase 1 — Core Experience
- 🌆 Full 3D cyber city (Overleague arena) loaded from embedded GLB
- 🤖 Chicken Bot robot with walk animation
- 🎮 WASD / Arrow key movement
- 📷 360° orbit camera — mouse look + scroll to zoom
- 🖱️ Click to lock mouse for free look

### Phase 2 — Full Experience
- 🎵 Procedural music — drums, bass, lead melody, chord pad (Web Audio API, no files)
- 📱 Mobile virtual joystick + touch camera controls
- 💬 Robot dialogue system — 5 trigger zones around the city
- 🌊 Terrain-following floor detection — robot walks on slopes and curves
- 🔊 Music toggle button (top-right) or press **M**

---

## 🕹️ Controls

### Desktop
| Key | Action |
|-----|--------|
| `W / A / S / D` | Move robot |
| `Arrow Keys` | Move robot |
| `Click` | Lock mouse for camera look |
| `Mouse Move` | Rotate camera (horizontal + vertical) |
| `Scroll Wheel` | Zoom in / out |
| `M` | Toggle music |

### Mobile
| Gesture | Action |
|---------|--------|
| Left joystick | Move robot |
| Drag right half of screen | Rotate camera |
| 🎵 button (top-right) | Toggle music |

---

## 💬 Robot Dialogue

As you explore, the robot (Chicken-Bot) talks to you at 5 locations around the city. Walk into each zone and a dialogue bubble appears at the bottom of the screen. Pick an answer — the robot responds — then the dialogue auto-dismisses. You keep walking the whole time, nothing is blocked.

| Zone | What the Robot Says |
|------|-------------------|
| Spawn (start line) | Welcomes you to Overleague Cyber City |
| Grandstands | Tells you about the 47,000 empty seats |
| Curved section | Comments on the track geometry |
| OVLA sign | Reveals it was robbed of a championship |
| Drone zone | Asks if you've ever ridden a drone |

---

## 🛠️ Technical Details

### Architecture
- **Single HTML file** — everything embedded, no folders, no external files
- **~17MB** total (GLBs encoded as base64 chunks)
- Works from `file://` protocol — no server needed

### 3D Engine
- **Three.js r128** — inlined from npm (no CDN dependency)
- **GLTFLoader** — inlined, no Draco compression (avoids WASM fetch issues)
- Both GLBs split into **32KB base64 chunks** to avoid browser `atob()` size limits

### GLB Assets
| Asset | Original | Notes |
|-------|---------|-------|
| `chicken_bot.glb` | 4.1MB | 1 mesh, 32 nodes, 1 walk animation |
| `overleague_cyber_city.glb` | 8.0MB | 205 meshes, 701 nodes, 30 materials |

### Music Engine
Pure Web Audio API — zero audio files. Four layers synthesised in real-time:
- **Kick drum** — oscillator with frequency sweep
- **Snare** — noise buffer with bandpass filter
- **Hi-hats** — noise buffer with highpass filter
- **Bass** — sawtooth oscillator with resonant lowpass sweep
- **Lead melody** — square wave, A-C-D-E phrase
- **Chord pad** — stacked sine waves, 4-bar loop

### Floor Detection
Raycaster shoots downward from robot position each frame. DoubleSide materials on all city meshes ensure hits from above. Smooth lerp (0.2) prevents jitter. Falls back to last known Y if no surface detected within 2.5 units below.

### Dialogue System
- 5 invisible trigger zones (sphere collision, radius 8–12 units)
- Typewriter text effect (22ms per character)
- Each zone fires once per session, 300-frame cooldown after dismiss
- Robot keeps walking — dialogue never blocks movement

---

## 📁 File Structure

```
cyber_city_phase2.html   ← The entire experience (single file)
README.md                ← This file
```

That's it. Two files.

---

## 🚀 How to Run

```bash
# Option 1: Just double-click the HTML file
# Opens in Chrome / Edge / Firefox

# Option 2: Local server (if browser blocks file:// protocol)
npx serve .
# Then open http://localhost:3000/cyber_city_phase2.html
```

---

## 🔧 Customisation

All key values are at the top of the `<script>` section:

```js
var CITY_SCALE = 0.08;   // city size
var BOT_SCALE  = 0.35;   // robot size
var SPEED      = 3.5;    // walk speed
var SPAWN_X    = -24.2;  // spawn position X
var SPAWN_Z    = -1.9;   // spawn position Z
var FLOOR_Y    = -3.65;  // spawn floor height
```

To add more dialogue, add objects to the `TRIGGERS` array:
```js
{
  id: 'unique_id',
  x: -10, z: -30, r: 10,   // position and trigger radius
  q: "Robot says this...",
  opts: [
    { label: "Option A", reply: "Robot replies A..." },
    { label: "Option B", reply: "Robot replies B..." }
  ]
}
```

---

## 🏗️ Built With

- [Three.js r128](https://threejs.org/) — 3D rendering
- Web Audio API — procedural music
- GLB models from [Sketchfab](https://sketchfab.com)
  - [Overleague Cyber City](https://sketchfab.com/3d-models/overleague-cyber-city-10b3b5fd93b04fc38cf117ebfb1b73d9) by amogusstrikesback2
  - Chicken Bot robot

---

## 📱 Browser Support

| Browser | Desktop | Mobile |
|---------|---------|--------|
| Chrome 90+ | ✅ | ✅ |
| Edge 90+ | ✅ | ✅ |
| Firefox 88+ | ✅ | ✅ |
| Safari 15+ | ✅ | ✅ |

> **Note:** Must be opened from Edge/Chrome locally. The Claude.ai preview panel blocks CDN scripts — this is expected and doesn't affect local use.

---

## 📄 License

Models belong to their original creators on Sketchfab. Code is free to use and modify.
EOF
echo "Done"
