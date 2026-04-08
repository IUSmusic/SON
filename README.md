# SON

Demo:
https://iusmusic.github.io/SON/

![Preview](/preview.png)

[![Status](https://img.shields.io/badge/status-active-black)](#)
[![License](https://img.shields.io/badge/license-all_rights_reserved-red)](./LICENSE)
[![Type](https://img.shields.io/badge/type-research_software-blue)](#)
[![Platform](https://img.shields.io/badge/platform-browser-lightgrey)](#)
[![Architecture](https://img.shields.io/badge/architecture-single--file-informational)](#architecture)
[![Audio](https://img.shields.io/badge/audio-Web_Audio_API-purple)](#technology-stack)
[![UI](https://img.shields.io/badge/ui-React_18-61dafb)](#technology-stack)
[![Visualization](https://img.shields.io/badge/visualization-Canvas_2D-orange)](#technology-stack)
[![Export](https://img.shields.io/badge/export-WAV-success)](#wav-export)
[![Domain](https://img.shields.io/badge/domain-space_weather-darkgreen)](#research-framing)

**SON** is a browser-based sonification environment for representing **coronal mass ejection (CME)** and **geomagnetic storm** events as synchronized sound, visual state, and derived physical metrics.

The repository is intentionally minimal: the full application is distributed as a **single HTML document** (`SON.html`) containing the interface, event catalog, sonification engine, visualization logic, and in-browser WAV export pipeline. The project is designed as a compact research, exhibition, and educational artifact rather than a large framework-dependent software stack.

---

## Contents

1. [Abstract](#abstract)
2. [Research Framing](#research-framing)
3. [Core Capabilities](#core-capabilities)
4. [Repository Structure](#repository-structure)
5. [Quick Start](#quick-start)
6. [Usage Workflow](#usage-workflow)
7. [Technology Stack](#technology-stack)
8. [Scientific and Sonification Model](#scientific-and-sonification-model)
9. [Event Catalog](#event-catalog)
10. [WAV Export](#wav-export)
11. [Implementation Notes](#implementation-notes)
12. [Limitations](#limitations)
13. [Roadmap](#roadmap)
14. [License](#license)
15. [Contact / Permissions](#contact--permissions)

---

## Abstract

SON formalizes a browser-native approach to **scientific sonification of extreme solar and geomagnetic events**. Instead of assigning arbitrary sounds to arbitrary values, the system converts curated CME and storm parameters into a layered audio structure informed by physically meaningful quantities such as coupling strength, dynamic pressure, magnetic orientation, magnetopause geometry, and storm indices.

The resulting application serves three roles simultaneously:

- a **research demonstrator** for interpretable data-to-sound mapping,
- a **science communication instrument** for public-facing presentation of heliophysics,
- and a **creative computational object** for performance, installation, or exhibition contexts.

---

## Research Framing

Space-weather events are usually communicated numerically, visually, or through textual forecasting products. SON explores a complementary question:

> How can solar-wind and geomagnetic event structure be translated into a browser-based audiovisual instrument while preserving interpretability, parameter traceability, and physically grounded control relationships?

The project therefore emphasizes:

- **parameter transparency** rather than opaque generative behavior,
- **derived physical estimates** rather than purely decorative mappings,
- **interactive inspection** alongside listening,
- and **lightweight deployment** suitable for classrooms, workshops, galleries, and GitHub-based distribution.

---

## Core Capabilities

- Curated event browser for historically significant and recent CME / geomagnetic storm cases
- Real-time sonification built with the **Web Audio API**
- Dual listening modes for **scientific** and **album-style** presentation
- Derived heliophysical and magnetospheric estimates computed directly in the client
- High-DPI **Canvas 2D** visualization synchronized with event state
- On-page metric inspector for inputs, estimates, and mapping relationships
- In-browser **30-second stereo WAV export** using `OfflineAudioContext`
- Portable, **no-build** architecture suitable for direct browser execution

---

## Repository Structure

```text
.
├── SON.html      # complete application: UI, event data, physics estimates, audio engine, visualization, WAV export
├── README.md     # repository documentation
└── LICENSE       # repository license terms
```

This repository intentionally avoids a multi-directory build layout. The objective is portability, inspectability, and ease of deployment.

---

## Quick Start

### Open directly in a browser

Clone or download the repository, then open:

```text
SON.html
```

in a modern desktop browser.

### Run with a lightweight local server

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/SON.html
```

### Recommended browsers

- Chrome / Chromium
- Edge
- Firefox
- Safari with modern Web Audio support

Because browser audio typically requires a user gesture, playback should be initiated from the interface after the page loads.

---

## Usage Workflow

1. Open `SON.html`.
2. Choose a CME / geomagnetic storm event from the event panel.
3. Inspect the displayed physical inputs and derived estimates.
4. Start audio playback in the selected listening mode.
5. Observe how event parameters affect both visual and auditory structure.
6. Export a rendered **30-second WAV** for archival, analysis, or DAW-based reuse.

---

## Technology Stack

### Runtime and interface

- **HTML5** packaging
- **React 18**
- **ReactDOM 18**
- **Babel Standalone** for in-browser JSX transpilation

### Audio and rendering

- **Web Audio API** for synthesis and real-time playback
- **OfflineAudioContext** for file rendering
- **Canvas 2D** for visualization

### Programming model

- Vanilla JavaScript for event definitions, calculation logic, parameter mapping, and rendering control
- CDN-loaded dependencies for frictionless distribution

---

## Scientific and Sonification Model

The application accepts event-level inputs such as:

- solar-wind speed `v`
- proton density `n`
- magnetic-field magnitude `B`
- southward magnetic component `Bz`
- geomagnetic indices `Kp` and `Dst`
- X-ray intensity
- event duration

From these, SON computes or estimates multiple physically motivated quantities, including:

- solar-wind **dynamic pressure**
- **IMF clock angle**
- **Newell coupling function**
- **Kan–Lee reconnection electric field**
- **Alfvén speed** and related characteristic speeds
- **magnetopause stand-off distance**
- **bow-shock distance**
- **plasmapause-related estimates**
- **storm-time Dst approximation**
- characteristic low-frequency and wave-process terms such as Pc1 / Pc5-style and Kelvin–Helmholtz-related estimates

### Mapping philosophy

The system is not a literal simulation of the magnetosphere. It is a **scientifically informed interpretive sonification engine**. Derived values are used as control signals for synthesis layers such as:

- low-frequency storm drone / ring-current style layers
- harmonic overtone structure
- noise texture and filtered turbulence bands
- modulation depth and rate
- waveshaping / distortion intensity
- master amplitude motion and envelope behavior

### Design principle

SON aims to preserve a meaningful relationship between domain variables and auditory change, so that sonic variation remains explainable rather than arbitrary.

---

## Event Catalog

The application includes a curated set of notable events ranging from modern space-weather cases to historically significant storms, including examples such as:

- the **May 2024 G5 storm**
- the **October 2024 G5 storm**
- the **March 2024 severe storm sequence**
- the **2023 and 2017 major flare / storm intervals**
- the **2012 near-miss superstorm**
- the **2003 Halloween storms**
- the **1989 Hydro-Québec blackout storm**
- the **1859 Carrington Event**

The repository uses a **curated event set**, not a live API feed. This makes the application stable, portable, and reproducible for demonstration and interpretation.

---

## WAV Export

SON includes browser-side audio rendering and file export.

### Export characteristics

- stereo output
- 16-bit PCM WAV encoding
- 30-second offline render
- generated in-browser without server-side processing

### Typical uses

- comparative listening studies
- archival examples for teaching
- integration with DAWs and sound-design workflows
- exhibition playback assets

---

## Implementation Notes

### Why a single-file architecture?

The project deliberately prioritizes:

- ease of sharing,
- ease of inspection,
- zero-install presentation,
- and compatibility with lightweight hosting environments.

### Why React without bundling?

React is used for interface composition, while Babel Standalone enables direct browser execution. This choice keeps the repository easy to read and run at the cost of conventional production bundling.

### Intended context

SON is best understood as:

- a research prototype,
- a communication instrument,
- and an exhibition-ready software artifact.

It is **not** intended as an operational forecasting tool or validated scientific analysis platform.

---

## Limitations

- The repository is distributed as a **single HTML file**, so code is not modularized into multiple source files.
- External libraries are loaded from CDNs rather than bundled locally.
- Event values are curated and simplified for interpretability and presentation.
- Some computed relationships are approximate and intended for explanatory sonification rather than rigorous predictive modeling.
- The application operates on event-level parameter sets rather than full continuous time-series ingestion.

---

## Roadmap

Potential future directions include:

- integration of live NOAA / NASA / mission-derived feeds
- time-series playback rather than event snapshots
- reproducible experiment presets and logging
- side-by-side mapping comparison modes
- modular separation of UI, physics, and synthesis code
- formal testing of derived-quantity functions
- GitHub Pages-oriented packaging using `index.html`

---

## License

This repository is **not open source**.

All rights are reserved by the copyright holder. No permission is granted to use, copy, modify, merge, publish, distribute, sublicense, sell, or create derivative works from the repository contents unless explicit prior written permission is provided.

See the [LICENSE](./LICENSE) file for the full terms.

---

## Contact / Permissions

For licensing, permissions, collaboration, exhibition use, or other repository-related inquiries, contact the repository owner.
