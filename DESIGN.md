# Quasar - Design Document

> Free, open source, Linux-first creative suite. Animate, code, build games, export to web. For everyone from beginners to veterans.

---

## Concept

Quasar is a spiritual successor to Adobe Flash and Macromedia Flash, built for Linux first and designed to make creative tools accessible to everyone. It is free, open source, and built around the idea of reviving the Flash era culture of accessible, expressive, one-tool-does-everything creativity.

The name comes from quasars, the brightest and most energetic objects in the known universe, which reflects the scope of what you can make with it.

---

## Philosophy

- **Free forever.** No subscription, no licence fee, no paywalled features.
- **Open source.** The community contributes features, fixes bugs, and extends the tool.
- **Linux first.** Then Windows and Mac once stable.
- **Modular.** Load only what you need. Light enough to run on modest hardware.
- **Beginner to veteran.** From block coding to raw scripting, from no-code to full code.
- **The official Quasar trailer will be made entirely inside Quasar.**

---

## Platform Targets

| Platform | Status |
|---|---|
| Linux (primary) | First target |
| Windows | After Linux is stable |
| macOS | After Windows |
| Web (browser-based lite version) | Natural extension of the web export pipeline |
| Mobile companion app | Tablet and stylus support for reviewing, annotating, and sketching |

---

## Tech Stack (Proposed)

- **Core engine:** C++ or Rust
- **GUI framework:** Qt (industry standard for cross-platform desktop apps)
- **Prototyping layer:** Python + PyQt (prototype first, rewrite performance-critical parts later)
- **Embedded scripting runtimes:** Multiple, see Scripting section

---

## Startup Workspace Selector

On launch, the user chooses which workspace to open. Only the relevant modules load, which keeps the software fast and focused.

**Workspace options:**
- Draw
- Animate
- Game Dev
- Draw + Animate
- Animate + Game Dev
- Everything

Each workspace loads only what it needs. Beginners are not overwhelmed, and advanced users can load everything if they want to.

---

## Feature Set

### Drawing Tools

There is no dedicated drawing workspace. Krita and GIMP already exist, are free, and handle this well. No point rebuilding what already works.

Instead, Quasar includes **inline bitmap editing**, which covers what animators actually need without leaving the software:

- Double click any bitmap asset and a lightweight editor opens right there inline
- Basic brush, eraser, fill, and eyedropper for quick fixes without switching applications
- Fix what you need, confirm, and you are straight back in your animation
- Familiar to Animate users since double clicking to enter a symbol is already an established pattern

**Also included:**
- Toggleable perspective grids: 1-point, 2-point, 3-point, isometric, and curved/fisheye
- Custom vanishing point placement anywhere on the canvas
- Straight or curved horizon lines
- Grids and guides for characters and scene composition
- Drawing tablet, stylus, and pen support as standard
- Built-in reference board: pin reference images in a dockable panel without ever leaving the software

---

### Animation Tools

**Timeline:**
- Frame-by-frame keyframing
- Keyframe notation types borrowed from Blender: extremes, breakdowns, in-betweens
- Timeline can display in frames, seconds, or BPM (beats and measures/ticks)
  - Input tempo and time signature for music-synced animation
- Symbols and nested symbols (buttons, graphics, movie clips, and more)

**Tweening:**
- Classic tween
- Shape tween with shape hints
- Motion tween
- Additional tween types to be confirmed
- Easing in and out with an extended preset library combining Animate and Blender easing options
- Custom easing curve editor (graph editor) for full mathematical control

**Onion skinning:**
- Toggle which frame types are visible: extremes only, breakdowns only, in-betweens only, or any combination

**Bone tools:**
- Standard IK (Inverse Kinematics) rigging
- **Sprite-aware IK:** a "sprite mode" toggle so the bone tool understands the art style and automatically cleans up pixels to stay consistent with the character
  - Option to supply a high-resolution version of the sprite for better reference
  - Option to supply a labelled sprite sheet: mark each body part once and the software understands the character's range of motion from that point forward
- Versatile enough to go beyond standard rigging use cases

**Camera:**
- Virtual camera system
- Perspective grid updating with camera movement (planned)

**Physics simulation:**
- Basic 2D physics for hair, cloth, and bouncing objects
- Define the parameters and let the software generate movement rather than keyframing it manually

**Auto lip sync:**
- Feed in an audio file, the software detects phonemes and suggests mouth shapes based on your defined mouth chart
- The user retains full final control

---

### Game Development Tools

Game dev feeds directly from the animation workspace. Assets and animations made in Quasar go straight into the game without any conversion step.

- Build 2D games using the same assets and animations created in Quasar
- Export to supported languages and formats
- Optional code obfuscation on export

---

### Coding and Scripting

**Three coding modes:**

1. **Standard scripting:** write code in a dedicated script editor. Supported languages include Python, C++, C#, Java, ActionScript 3, JavaScript, and more via extensions.
2. **Frame and symbol actions:** go into specific keyframes or symbols and write code directly, exactly like the Actions panel in Flash and Animate. Essential for Flash-style projects and for anyone modding Flash-based games.
3. **Block coding:** a visual node and block connector system similar to Scratch or Unreal Blueprints. A full alternative to text-based coding, not a simplified version of it.

**Supported languages (built-in):**
- ActionScript 3
- Python
- JavaScript
- More available via downloadable extension packs

**Multi-runtime system:**
- Each language runs through its own embedded runtime
- No forced transpilation. The software defaults to whichever language the user wrote in.

**Extension system:**
- Download additional language support packs separately
- The community can contribute new runtimes and extensions
- Keeps the base install lean

---

### Audio Editor (Built-in)

A lightweight audio editor built directly into Quasar. Think a stripped-down Audacity or Adobe Audition, covering what animators and game developers actually need.

- Trim, cut, and layer audio
- Basic effects
- Channel panning: choose which channels audio is sent to
- Surround sound support (5.1 and beyond)
- BPM and tempo tools tied directly to the animation timeline

---

### Collaboration

- **Real-time collaborative editing:** multiple people can work in the same project file simultaneously, similar to Google Docs but for animation
- Team members can work on different scenes at the same time
- Built with indie animation team workflows in mind

---

### AI Assist (Local Only)

- Powered by a local AI model that the user installs themselves, keeping all data on their own machine
- Not a generative or "do it for me" tool
- Functions as an assistant:
  - Explains how parts of the codebase work
  - Breaks down how a problem could be approached
  - Provides pseudocode to work from
  - The user still does the actual work
- Nothing is sent to external servers

---

### Session and History

- **Persistent undo and redo history:** survives closing and reopening a file
- **Built-in time-lapse recording:** every stroke and action is recorded automatically in the background
  - Export as a time-lapse video at any point
  - The same action log that powers time-lapse is what enables persistent undo history, so both features share one implementation

---

### Export Formats

**Images:**
- JPEG, PNG, GIF, SVG, WebP, BMP, AVIF, RAW
- PSD (Photoshop), ASE, Aseprite (.ase / .aseprite)

**Video:**
- MP4, MOV, AVI, MKV, WebM
- Lossless format options for maximum quality output
- Codec and compression tools

**Game and code export:**
- Export to any supported language
- Optional code obfuscation on export

**Other:**
- JSON (for web playback via the Quasar Player)
- APNG, animated GIF
- SWF import (simplified, to support Flash project migration)

---

### Community and Ecosystem

- **Built-in community asset library:** browse, download, and share brushes, palettes, symbols, rigs, and more directly inside the software
- **Shareable hotkey profiles:** so users migrating from Animate or other tools can feel at home straight away
- **Batch render queue:** line up multiple projects to export in one go
- Open source by nature: the community contributes features, fixes, and optimisations organically

---

## UI Themes

Quasar has a built-in theme system with preset themes and full custom theme support. The software should never look like a generic grey corporate tool.

**Default theme: Galaxy.** Deep space, cosmic, and fitting for the Quasar name. The first thing you see when you open it.

**Preset themes at launch:**
- **Galaxy** (default): deep space, stars, cosmic energy
- **Frutiger Aero:** glossy, glass-effect, nature-tinged, early 2010s nostalgia
- **Pop:** bubbly, pastel, rounded, and sparkly. Y2K meets kawaii. A lot of people are going to like this one.
- **Windows XP:** the classic Luna theme, iconic teal, green, and silver
- **Windows Vista:** full Aero Glass with translucency and dark chrome
- **Windows Longhorn:** the Vista prototype codename. Experimental early Aero Glass turned up to maximum. Niche, but the people who recognise it will love it.
- **Windows 7 (Vienna):** refined Aero Glass, widely considered the peak of that design era
- Dark mode (standard)
- Light mode (standard)
- High contrast (accessibility)

**Custom themes:**
- Full open documentation on how to build your own themes
- Community theme sharing via the asset library
- Fully customisable: colours, accents, borders, and everything else

---

## Sound Design

Quasar has a full sound identity. Nothing should be silent, everything should feel alive.

**UI sounds include:**
- Startup sound
- Shutdown sound
- Workspace selection sounds: each workspace has its own distinct audio cue
- Export and compile completion sound
- General UI interaction sounds for toggles, clicks, and notifications

**Sound presets:**
- **Galaxy** (default): cosmic, spacious sound design
- **Windows Longhorn:** the prototype sounds that never officially shipped. A very specific kind of nostalgia.
- **Windows XP:** the classics that are burned into an entire generation's memory
- **Pop:** bubbly and cute, matches the Pop theme
- **Silent:** for people who prefer it that way

**Custom sound packs:**
- Full documentation for creating and sharing custom sound packs
- Community sound pack sharing via the asset library
- Every individual sound can be toggled on or off

---

## Distribution

- **Newgrounds:** the first place this should be posted. The Flash community lives here and this is essentially a homecoming.
- YouTube devlogs documenting the build process, building an audience before launch
- Bluesky, Tumblr, TikTok, Twitter/X, Instagram
- itch.io
- GitHub
- A dedicated website eventually

---

## The Pitch

"Scratch's accessibility. Flash's creative freedom. Animate's animation tools. On Linux. Free. Open source. Forever."

---

*Full feature specification compiled from a single brainstorming session. Subject to change as development progresses.*
