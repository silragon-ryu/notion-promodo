# 🕐 Observation Deck

> A cyberpunk Pomodoro timer — single HTML file, zero dependencies, runs anywhere.

![Observation Deck](https://img.shields.io/badge/version-1.0-00d4ff?style=flat-square&labelColor=06060f)
![HTML](https://img.shields.io/badge/html-single%20file-bf00ff?style=flat-square&labelColor=06060f)
![No dependencies](https://img.shields.io/badge/dependencies-none-00ff9d?style=flat-square&labelColor=06060f)
![License](https://img.shields.io/badge/license-MIT-ff00aa?style=flat-square&labelColor=06060f)

---

## Preview

```
╔══════════════════════════════════════════╗
║ [OBSERVATION DECK]       SYSTEM NOMINAL  ║
╠══════════════════════════════════════════╣
║                                          ║
║ > START       (25:00)        TIMER       ║
║               FOCUS          STATUS      ║
║               BREAK 5m       BG          ║
║ R RESET                      VOICE       ║
║               o o o o                    ║
║                                          ║
╚══════════════════════════════════════════╝
```

---

## Features

### ⏱ Pomodoro Timer
- 60fps smooth ring animation driven by `requestAnimationFrame` — no CSS transition lag
- Focus and break segments with seamless auto-transition
- Session dots track your current pomodoro cycle (4-round grouping)
- Session count and total focus time tracked in the footer

### ⚡ Smart Auto-Break
- Break duration is automatically calculated from focus time — **1 min per 5 min of focus** (min 3m, max 30m)
- Manual override available: nudge with `−`/`+` or type a value directly
- Badge shows `⚡ AUTO` or `✎ MANUAL` state — click to reset back to auto at any time
- Changing focus duration recalculates break only when in auto mode — your manual override is never overwritten

### 🎙 Custom Voice Alerts
- Spoken announcements at the end of every focus session and break
- Full **Voice Settings panel** — search and select from every TTS voice installed on your system
- Tune **Pitch**, **Rate**, and **Volume** independently with live sliders
- **Test button** — hear your exact settings before saving
- Settings persist via `localStorage` across sessions
- Works with Japanese voices (`Kyoko` on macOS, `Haruka` on Windows) for a natural JP-accented delivery
- Graceful fallback to best available English voice if no Japanese voice is installed

### 🖼 Custom Background
- Drag and drop any image or GIF onto the widget
- Or click the **BG** button to open a file picker
- Subtle parallax effect on mouse move

### ◎ Focus Mode
- Intensifies the neon glow for a more immersive session
- Toggle with the sidebar button or press `F`

### ⌨️ Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `Space` | Play / Pause |
| `R` | Reset timer |
| `F` | Toggle focus mode |

---

## Quick Start

No build step. No npm. No config.

```bash
git clone https://github.com/yourusername/observation-deck.git
cd observation-deck
open observation-deck.html   # macOS
# or just double-click the file in your file manager
```

Or drop it into any static host:

```
observation-deck/
└── observation-deck.html    ← that's it
```

---

## Embedding in Notion

link:https://promodo-widget.netlify.app/

---

## Timer Configuration

Open the **⏱ TIMER** panel from the sidebar to configure:

| Setting | Default | Range |
|---------|---------|-------|
| Focus duration | 25 min | 1–300 min |
| Break duration | Auto (5 min) | 1–60 min |

**Quick presets:** 15m · 25m · 45m · 60m · 90m

---

## Voice Setup

The widget uses the **Web Speech API** — voices come from your OS and browser.

### Installing Japanese Voices

**macOS**
1. System Settings → Accessibility → Spoken Content → System Voice
2. Click **Manage Voices...** → Japanese → download `Kyoko` (recommended) or `O-Ren`

**Windows**
1. Settings → Time & Language → Language → Add a language → Japanese
2. During install, ensure **Text-to-speech** is checked
3. Best voice: `Haruka`

**Chrome / Edge (any OS)**
1. `chrome://settings/` → Advanced → Accessibility → Manage TTS voices
2. Download Japanese voices from the list

### Selecting Your Voice

1. Click **🎙 VOICE** in the sidebar
2. Search by name or language code (e.g. `ja`, `ko`, `en-GB`, `fr`)
3. Select a voice — `⬡` means local/offline, `☁` means network-streamed
4. Adjust pitch, rate, and volume
5. Hit **▶ TEST** to preview
6. Click **SAVE** — your choice is remembered across sessions

---

## Customisation

Everything lives in a single file. Open `observation-deck.html` in any text editor.

**Colours** — edit the CSS variables at the top of `<style>`:
```css
:root {
  --blue:   #00d4ff;   /* ring, accents */
  --purple: #bf00ff;   /* secondary glow */
  --pink:   #ff00aa;   /* pause state */
  --green:  #00ff9d;   /* break mode */
  --bg:     #06060f;   /* background */
}
```

**Voice lines** — edit `BREAK_LINES` and `FOCUS_LINES` arrays in `<script>`:
```js
const BREAK_LINES = [
  "Otsukaresama deshita. You did well. Please rest now.",
  // add your own...
];
```

**Auto-break formula** — edit `autoBreak()`:
```js
function autoBreak(fm){
  return Math.min(30, Math.max(3, Math.round(fm / 5)));
  // fm = focus minutes. Default: 1 min break per 5 min focus.
}
```

---

## Browser Support

| Browser | Timer | Voice | Notes |
|---------|-------|-------|-------|
| Chrome 90+ | ✅ | ✅ | Best experience |
| Edge 90+ | ✅ | ✅ | Same as Chrome |
| Firefox 90+ | ✅ | ✅ | Fewer TTS voices available |
| Safari 15+ | ✅ | ✅ | macOS voices work great |

Voice requires a user interaction (clicking Start) before the browser allows audio — this is a browser security requirement, not a bug.

---

## Stack

| | |
|--|--|
| **Framework** | None |
| **Animation** | `requestAnimationFrame` + `performance.now()` |
| **Voice** | Web Speech API (`SpeechSynthesisUtterance`) |
| **Fonts** | [Orbitron](https://fonts.google.com/specimen/Orbitron) · [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) (Google Fonts CDN) |
| **Storage** | `localStorage` (voice settings only) |
| **Dependencies** | Zero |
| **File count** | 1 |

---

## License

MIT — do whatever you want with it.

---

<p align="center">
  <sub>built with neon and focus</sub>
</p>
