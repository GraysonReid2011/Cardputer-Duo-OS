# Cardputer Duo OS

**A dual-device handheld interface for the M5Stack Cardputer ADV and a CYD-class display.**

Cardputer Duo OS pairs the Cardputer ADV’s keyboard and microSD storage with a secondary CYD display over UART. The Cardputer handles input, app management, and files; the CYD mirrors the launcher and app screens. The goal is a small, customizable handheld environment where you can use built-in tools and create or edit apps on the device without reflashing firmware for every change.

## The interface

**Home** is the app launcher. Browse built-in apps and SD-card apps with the Cardputer keyboard, filter by category, and search by app name or category. Recently used apps appear near the top of search results. Apps can be pinned and reordered, and the CYD mirrors the visible launcher entries and selection.

**Scripts** is the SD-card file browser for `.duo` apps. Select a script to run it on both displays, open it in the editor, create a new script, or copy, rename, and delete files. The Cardputer’s SD card is the source of truth for scripts and saved app data.

**Templates** installs editable example apps onto the Cardputer’s SD card. Templates are starting points: install one, open it in Script Pad, and adapt its screens, controls, and behavior.

## Built-in apps

- **App Search** filters the app catalog by title or category and launches the selected result. SD-card apps can also be opened directly in Script Pad for editing.
- **System Status** shows the CYD link status, SD-card availability, and the number of scripts found.
- **Settings** controls the shared accent color and light or dark appearance. Its Bluetooth Settings menu can select a board radio, enable it, scan for devices, and connect to a saved speaker.
- **Canvas** lets you choose a color, place tiles with Enter, and clear the drawing.
- **Counter** provides keyboard-operated controls to change a value, toggle wrapping, and view progress.
- **Calculator** is a keyboard-navigated 4×4 keypad for entering digits and choosing operations.
- **Stopwatch** supports start, pause, reset, and lap timing, with recent lap splits mirrored to both displays.
- **Timer** lets you set minutes and seconds, start or pause the countdown, and reset to a saved preset.
- **Palette Studio** browses colors and applies a selection to a preview card.
- **Script Guide** provides on-device help for navigation, editing, script controls, saved state, and drawing commands.
- **Script Pad** edits `.duo` files directly on the Cardputer. It includes line numbers, syntax highlighting, find, undo and redo, validation feedback, and preview on both displays. Unsaved changes prompt you to save, discard, or continue editing.
- **Music Player** plays MP3 files from the SD card’s `music` folder. On supported Cardputer ADV builds, audio can play through the Cardputer speaker or stream to a compatible Bluetooth device through the CYD.

## Custom apps on the SD card

Create `.duo` scripts on the Cardputer or edit them on a computer and place them in `/scripts`. Add metadata such as `# APP`, `# ABOUT`, `# CATEGORY`, and `# COLOR` to register a script in Home with a name, description, category, and tile color.

The script language supports keyboard input, menus, tabs, buttons, sliders, checkboxes, radio choices, confirmation dialogs, variables, conditional logic, loops, app navigation, and saved per-app state. Drawing commands create shared screens with text, panels, shapes, lines, and progress bars. Shared theme settings let apps use or update the common palette. The on-device Templates gallery includes examples such as Pocket Organizer, Tabbed Notebook, App Hub, Duo Dashboard, Theme Studio, and reusable GUI controls.

## Hardware roles and project status

The Cardputer ADV remains the keyboard and SD-card host. The CYD is a secondary display connected over UART, and its screen follows the Cardputer’s current app and selection. **CYD touchscreen input is currently disabled**; use the Cardputer keyboard to navigate and control apps.

Cardputer Duo OS is an actively developed firmware prototype. Board revisions and display configurations can vary, so check the project’s wiring and build notes for the assumptions used by each target.
