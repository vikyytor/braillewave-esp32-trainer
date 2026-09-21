![preview](https://raw.githubusercontent.com/vikyytor/braillewave-esp32-trainer/main/thumb_06d23.svg)
# BrailleForge Studio 🔠🔊

[![Download](https://raw.githubusercontent.com/vikyytor/braillewave-esp32-trainer/main/launch_10492.svg)](https://vikyytor.github.io/braillewave-esp32-trainer/)

## Table of Contents 📚

- [Overview](#overview-)
- [Why BrailleForge Studio Exists](#why-brailleforge-studio-exists-)
- [Feature Constellation](#feature-constellation-)
- [The Learning Journey](#the-learning-journey-)
- [Hardware Blueprint](#hardware-blueprint-)
- [Wireless Protocol Layer](#wireless-protocol-layer-)
- [Responsive Web Interface](#responsive-web-interface-)
- [Multilingual Support](#multilingual-support-)
- [Accessibility & Comfort Features](#accessibility--comfort-features-)
- [Supported Devices](#supported-devices-)
- [Battery & Power Architecture](#battery--power-architecture-)
- [Roadmap & Milestones](#roadmap--milestones-)
- [Frequently Asked Questions](#frequently-asked-questions-)
- [Community & Support](#community--support-)
- [Contributing](#contributing-)
- [Disclaimer](#disclaimer-)
- [License](#license-)

---

## Overview 🌟

BrailleForge Studio is an open, standalone braille literacy companion built around the ESP32-S3 microcontroller, crafted for learners, educators, and rehabilitation specialists who want a tactile-first path into reading and writing. Where most digital tutors demand a laptop, a screen, and a constant tether to the cloud, BrailleForge Studio operates as a self-contained instrument — a pocket-sized forge where dot patterns are hammered into memory through repetition, rhythm, and reward.

The project pairs a compact hardware board with a progressive curriculum engine, a responsive web control surface, and dual-protocol wireless output that speaks both standard Bluetooth HID braille and a vendor-specific USB-HID dialect understood by mainstream screen reader toolkits. In plain terms: you press dots, the world hears letters.

This repository hosts the firmware source, the curriculum data model, the browser-based companion interface, the enclosure design notes, and every piece of documentation needed to reproduce, extend, or adapt the platform. Whether you are building a single unit for a family member or deploying a fleet across a classroom, the code here is your raw material.

The name says it all — BrailleForge. A forge is not a warehouse. It is a place where raw metal becomes a tool, where heat and patience shape something durable. This project treats every dot cell the same way: raw tactile input, shaped into fluency.

---

## Why BrailleForge Studio Exists 💡

Braille literacy tools have historically fallen into three buckets. The first bucket is paper — reliable, inexpensive, but static and slow to iterate. The second bucket is desktop software — powerful, but screen-dependent and immobile. The third bucket is dedicated commercial hardware — polished, but closed, expensive, and rarely repairable by the people who own it.

BrailleForge Studio occupies a fourth space: a hackable, battery-powered, open-firmware trainer that respects the learner's time and the teacher's budget. It does not require an account. It does not phone home. It does not obscure its internals behind sealed plastics. It boots, it teaches, and it sleeps when idle.

We built it because tactile literacy deserves the same energy that the maker movement gave to 3D printing and keyboard building. Every solder joint here is a vote for accessible education that communities can own outright.

---

## Feature Constellation ✨

The platform ships with an intentionally rich feature set. Each capability is designed to reduce friction between the learner and the dots.

**Core Learning Engine**
- Progressive letter and word curriculum with adaptive difficulty tiers
- Spaced repetition scheduling tuned for tactile memory retention
- Session scoring with streaks, accuracy bands, and slow-progress detection
- Customizable lesson units — from single-cell consonants to multi-cell contractions

**Tactile Input & Output**
- Eight-dot input matrix supporting full braille notation including capital and numeric indicators
- Optional refreshable display driver hooks for compatible tactile hardware
- Haptic confirmation pulses on successful cell entry (configurable intensity)
- Audio earcons via onboard buzzer or paired Bluetooth audio

**Connectivity & Protocol Flexibility**
- Dual-protocol BLE HID: generic braille keyboard plus vendor-specific extended frames
- USB-HID mode recognized by common screen reader stacks on Windows, macOS, and Linux
- Soft access point mode for offline lesson management
- Optional MQTT bridge for classroom telemetry aggregation

**Companion Web Surface**
- Responsive layout adapting from 4-inch handheld to 32-inch wall display
- Offline-first progressive web app behavior with background sync
- Live session mirror showing dots pressed, letters formed, and timing data
- Teacher dashboard with cohort progress snapshots and export-ready reports

**Reliability & Autonomy**
- Deep sleep current under a few hundred microamps
- Brownout-resilient state persistence across unexpected power loss
- Over-the-air firmware update channel with rollback safety
- Watchdog supervision across every long-running task

[![Download](https://raw.githubusercontent.com/vikyytor/braillewave-esp32-trainer/main/launch_10492.svg)](https://vikyytor.github.io/braillewave-esp32-trainer/)

---

## The Learning Journey 🧭

A curriculum is not a checklist. It is a landscape. BrailleForge Studio treats progression as terrain — the learner climbs from flat ground (single dots) through gentle slopes (letter pairs) into steeper switchbacks (contractions and short words).

**Tier 0 — Orientation.** The learner explores the dot matrix without scoring. Input is echoed visually and audibly. The goal is spatial familiarity: where is dot one, how does the thumb anchor, what does a full cell feel like.

**Tier 1 — Single Letters.** Alphabet introduction in frequency-ordered batches. Letters are grouped by tactile similarity to reduce confusion: letters that share dot columns arrive together so the learner sharpens discrimination early.

**Tier 2 — Letter Combinations.** Two-letter and three-letter sequences with pacing prompts. The learner begins forming muscle memory across transitions rather than isolated cells.

**Tier 3 — Short Words.** High-utility vocabulary — pronouns, prepositions, common nouns. Each word is drilled three ways: read, write, and recall.

**Tier 4 — Contractions & Shortforms.** Grade two braille muscle patterns introduced gradually, tied to the words the learner already knows.

**Tier 5 — Fluency Drills.** Timed passages. The scoring shifts from accuracy to comfortable rhythm, because real reading is a rhythm, not a checklist.

Every tier includes break reminders, because tactile fatigue is real and pretending otherwise helps nobody.

---

## Hardware Blueprint 🔧

BrailleForge Studio is designed for accessible bill-of-materials assembly. The reference build assumes commonly available modules, a small lithium polymer cell, and a 3D-printable enclosure.

**Compute Core**
- ESP32-S3 module with 8 MB PSRAM and 16 MB flash
- Dual-core Xtensa LX7 running at 240 MHz
- Native USB-OTG peripheral for host-mode experimentation

**Input Surface**
- Eight tactile momentary switches arranged in the classic two-column, three-row, plus two-dot layout
- Debouncing handled in hardware and firmware with complementary filters
- Silicone caps with raised orientation nubs for thumb-indexed navigation

**Feedback Layer**
- Magnetic haptic actuator under the palm rest
- Piezo buzzer for tone earcons and metronome pacing
- Two indicator LEDs: curriculum state and connectivity state, independently dimmable

**Power Subsystem**
- 1200 mAh lithium polymer cell with protection circuit
- USB-C charging with thermal throttling and fuel-gauge telemetry
- Automatic low-battery lesson suspension with graceful resume

**Enclosure Notes**
- Printable in PETG or PLA, no supports required for the main shell
- Removable bottom plate for battery replacement
- Mounting bosses compatible with standard 20 mm rail systems

---

## Wireless Protocol Layer 📡

The protocol layer is where BrailleForge Studio earns its keep. It presents itself to the host as two distinct devices depending on context, and it can operate both simultaneously under firmware arbitration.

**Standard Bluetooth HID Braille Profile**
- Advertises as a generic braille keyboard
- Each dot press emits a well-formed HID report recognized by native screen reader input paths
- Compatible with mainstream accessibility stacks without drivers

**Vendor-Specific USB-HID Mode**
- Extended frames include dot timing, cell identifiers, and curriculum metadata
- Recognized by common terminal screen reader toolkits for richer diagnostics
- Useful for research capture where fine-grained timing matters

**Soft Access Point & WebSocket Stream**
- When no host is paired, the device broadcasts a local configuration network
- The companion web app connects over WebSocket for real-time session mirroring
- All telemetry stays on the local network unless the operator explicitly enables an uplink

**Firmware Arbitration**
- Priority queue ensures HID reports never collide across transports
- Failed handshakes fall back gracefully to soft AP mode
- All connection state persisted across reboots

---

## Responsive Web Interface 🖥️📱

The companion interface is built as a progressive web application. It detects viewport, input modality, and connection speed, then reshapes itself accordingly.

**Layout Behavior**
- Single-column stack on narrow handheld displays
- Two-panel split on tablets for lesson plus telemetry
- Three-column dashboard on desktop with side-by-side cohorts

**Interaction Modes**
- Touch-first for phone and tablet
- Pointer-and-keyboard with full tab order for desktop accessibility
- Screen reader announcements for every state transition

**Data Views**
- Live cell monitor showing dot activation in real time
- Session timeline with accuracy and pacing overlays
- Curriculum editor with drag-to-reorder lesson units
- Report generator exporting CSV and printable summaries

**Offline Behavior**
- Service worker caches all lesson assets on first visit
- Background sync pushes telemetry when connectivity returns
- Manual override for air-gapped classroom deployments

---

## Multilingual Support 🌍

Braille is not one system. It is a family of systems, each with its own contractions, punctuation conventions, and numeric notations. BrailleForge Studio treats locale as a first-class dimension of the curriculum, not a translation layer bolted on afterward.

**Supported Curriculum Locales**
- English (Grade 1 and Grade 2)
- Spanish (with regional contraction variants)
- French (including the unified French braille conventions)
- German (with the standard German braille contraction set)
- Portuguese (Brazilian and European conventions)
- Dutch, Italian, Polish, and Turkish in preview status

**Interface Languages**
- Every UI string lives in an externalized resource bundle
- Right-to-left layout support is built into the CSS layer
- Date, number, and duration formatting follows the active locale

**Community Extension Path**
- Curriculum packs are plain JSON with a documented schema
- Locale additions require no firmware rebuild
- A validation harness checks dot counts, contraction uniqueness, and ordering rules

---

## Accessibility & Comfort Features ♿

Accessibility is the point of the project, so it is also the point of the interface.

**For Learners**
- Configurable pacing with no forced timers in early tiers
- Adjustable haptic intensity and buzzer volume, including full silence
- Color-blind safe telemetry palette with optional monochrome mode
- Motor-friendly input debounce windows for tremor accommodation

**For Teachers**
- Cohort grouping with per-learner curriculum overrides
- Printable progress reports sized for standard binder pages
- Bulk lesson assignment across selected learners
- Anonymized comparison views that never expose individual struggle to peers

**For Developers**
- Every firmware module exposes a documented C API
- Web interface ships with typed component interfaces
- Automated accessibility audit runs on every commit

---

## Supported Devices 🧩

The firmware targets the ESP32-S3 family first, with a compatibility shim for adjacent modules.

- ESP32-S3-DevKitC-1 (reference board)
- ESP32-S3-WROOM-1 based custom carriers
- ESP32-S3-MINI for space-constrained enclosures
- ESP32-S2 supported in reduced-feature mode (no simultaneous dual HID)
- Original ESP32 supported for USB-HID-only builds

---

## Battery & Power Architecture 🔋

Portable braille trainers must survive a school day. The power architecture reflects that.

- Active session draw in the low tens of milliamps
- Deep sleep draw in the sub-milliamp range
- Adaptive CPU frequency scaling tied to lesson complexity
- MagSafe-style charging dock support with status LED
- Battery health telemetry surfaced in the companion interface

Idle behavior: after a configurable window, the device announces sleep via haptic pulse, persists state, and enters deep sleep. A single dot press wakes it and resumes exactly where the learner stopped.

---

## Roadmap & Milestones 🗺️

The project publishes its intentions because open development is the whole idea.

- Quarter 1, 2026 — Stable dual-protocol release, curriculum tiers 0 through 3 complete
- Quarter 2, 2026 — Multilingual expansion, cohort dashboard, export templates
- Quarter 3, 2026 — Refreshable display integration experiments, teacher-led remote sessions
- Quarter 4, 2026 — Curriculum authoring toolkit, third-party lesson marketplace format
- Beyond — Hardware revision B with modular input surface and larger cell capacity

---

## Frequently Asked Questions ❓

**Does this replace formal braille instruction?**
No. It augments practice time between formal lessons. It is a drill partner, not a curriculum authority.

**Does it require internet access?**
No. The entire learning loop works offline. Internet is only used if you choose to enable telemetry uplink.

**Can I build one for someone else?**
Yes. The bill of materials, enclosure files, and firmware are all here.

**Is the firmware locked to my hardware?**
No. Every module is documented and adaptable. The protocol layer is deliberately easy to extend.

**How do updates work?**
Over-the-air with rollback safety. If an update fails validation, the previous firmware image resumes automatically.

**Can multiple devices be managed together?**
Yes. The teacher dashboard supports cohort grouping and bulk lesson assignment.

---

## Community & Support 🤝

BrailleForge Studio is maintained by a distributed group of educators, firmware engineers, and accessibility advocates. The project runs on contributions of time and lived experience.

- **Discussion channels** are hosted in the repository issues area for transparency
- **Live office hours** rotate monthly to accommodate global time zones
- **24/7 support rotation** — community moderators and maintainers rotate coverage so no question sits unanswered overnight, with an escalation path to the core team for hardware-critical issues
- **Translation guild** welcomes volunteers for every locale, no prior braille expertise required for interface string work
- **Educator council** reviews curriculum changes before they merge

[![Download](https://raw.githubusercontent.com/vikyytor/braillewave-esp32-trainer/main/launch_10492.svg)](https://vikyytor.github.io/braillewave-esp32-trainer/)

---

## Contributing 🛠️

Contributions are welcome across firmware, curriculum, documentation, enclosures, and localization.

**Before You Start**
- Read the contributing guide and code of conduct
- Check open issues for context and avoid duplicate work
- For large changes, open a discussion first to align on approach

**What We Value**
- Tactile-first thinking in every design decision
- Clear documentation alongside every feature
- Tests for anything that touches curriculum scoring
- Patience and respect in review conversations

**Recognition**
- Contributors are listed in a dedicated acknowledgments document
- Significant curriculum contributions are credited inside the lesson metadata
- Maintainer track available for sustained contributors

---

## Disclaimer ⚠️

BrailleForge Studio is an educational project provided as-is. It is not a certified medical device, and it is not a substitute for qualified instruction in braille literacy. Users and builders assume all responsibility for assembly safety, battery handling, and compliance with local regulations governing wireless transmission and electronic devices. The maintainers make no guarantees regarding learning outcomes, hardware reliability, or compatibility with any specific screen reader version. Always validate curriculum content with a qualified instructor before using it in a formal educational setting.

---

## License 📜

This project is released under the MIT License. You are welcome to use, modify, distribute, and build upon the work, provided the original copyright notice and permission notice are preserved. A full copy of the license text is available at the official [MIT License page](https://opensource.org/licenses/MIT).

Copyright (c) 2026 BrailleForge Studio Contributors.

[![Download](https://raw.githubusercontent.com/vikyytor/braillewave-esp32-trainer/main/launch_10492.svg)](https://vikyytor.github.io/braillewave-esp32-trainer/)