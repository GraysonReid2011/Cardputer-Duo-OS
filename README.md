Here’s a paste-ready README draft. I’ve described CYD Bluetooth audio as experimental because the connection flow is still being worked on.
Cardputer Duo OS
Cardputer Duo OS is a two-board firmware project that turns an M5Stack Cardputer ADV and a CYD display into a small, keyboard-first app platform. The Cardputer runs the launcher, reads the SD card, and handles user input. The CYD acts as a second display, mirroring menus and app screens over a serial link.

The project is built with ESP-IDF. It includes built-in apps, a script editor, customizable SD-card apps, settings, and a shared GUI toolkit. Touch input is disabled; you navigate with the Cardputer keyboard.
Development status: This is an actively developed hobby firmware project, not a finished release. Bluetooth audio through the CYD is experimental and may not connect reliably yet.

What it can do
- Show a launcher and app screens on both the Cardputer and CYD.
- Navigate menus and apps from the Cardputer keyboard.
- Read and run .duo scripts from the Cardputer’s microSD card.
- Edit, preview, and create scripts with the built-in Script Pad.
- Register scripts as apps on Home using simple metadata.
- Save app settings and script state on the Cardputer SD card.
- Customize shared colors and the dark or light appearance.
- Scan for Wi-Fi networks and manage network settings.
- Play MP3 files from the SD card through the Cardputer speaker.
- Experiment with Bluetooth device scanning and CYD Bluetooth Classic audio.
Built-in apps
App	What it does
App Search	Search the launcher by app name or category and open an app.
Calculator	Use an on-screen keypad with keyboard navigation.
Canvas	Place colored tiles on a simple drawing canvas.
Counter	Adjust a saved counter and configure whether it wraps at its limits.
Music Player	Browse MP3 files in /music and play them through the Cardputer speaker. CYD Bluetooth audio output is experimental.
Palette Studio	Choose a color and preview it.
Script Guide	Read on-device help for the launcher and script language.
Script Pad	Create, edit, save, validate, and preview .duo apps.
Settings	Change shared colors and appearance, and access network and Bluetooth settings.
Stopwatch	Run a stopwatch and track lap times.
System Status	Check link, SD-card, and system status.
Templates	Browse and install starter script apps.
Timer	Set and run a countdown timer.


Custom script apps
Scripts are stored on the Cardputer SD card in /scripts. A .duo script can appear as an app on Home by including metadata such as:
# APP: Personal Color
# ABOUT: PICK A COLOR WITH TEXT INPUT
# CATEGORY: creative
# COLOR: 20C8FF
The Script Pad can edit and preview scripts on the device. You can also edit them on a computer and copy them to the SD card.

The .duo language includes commands for:
- Drawing text, panels, rectangles, lines, circles, and progress bars.
- Showing keyboard-operated menus, grids, tabs, buttons, sliders, checkboxes, radio choices, and confirmation dialogs.
- Reading typed input and branching based on selections or values.
- Using numeric and text variables, loops, conditions, reusable sections, and app-to-app navigation.
- Saving and loading per-app state and shared theme colors.
Script apps draw on a shared logical canvas and mirror their interface to the CYD. Runtime limits keep scripts bounded, and errors can report the failing line.
Starter apps in Templates
Templates provides editable examples including App Hub, Countdown Timer, Duo Dashboard, Focus Cycle, GUI Showcase, Level Settings, Line Chart, Native Tool Deck, Panel Gallery, Personal Card, Pocket Organizer, Progress Dashboard, Quick Notes, Radio Presets, Reusable Sections, Script Counter, Tabbed Dashboard, Tabbed Notebook, Task List, and Theme Studio.

These templates demonstrate things like saved notes and profile details, task tracking, progress displays, custom themes, reusable screen sections, and multi-page interfaces.
Controls
The Cardputer is the primary input device. In menus, the punctuation keys are mapped as directional controls:
- ; — up
- , — left
- . — down
- / — right
- Enter — select
- Backspace — back
- Fn + backtick — exit an app or stop a running script
The built-in Cardputer keyboard is also used for text entry in Script Pad and script apps.
Hardware and wiring
The firmware is designed for an M5Stack Cardputer ADV paired with a CYD-class ESP32 display board. The Cardputer owns the SD card and keyboard; the CYD is a secondary display. The common setup uses two 3.3 V UART signal wires:
Cardputer ADV Grove	CYD
GPIO1 TX	P3 GPIO35 RX
GPIO2 RX	P5 GPIO1 TX
GND	GND


Power both boards separately over USB. Do not connect the Grove 5 V pin to the CYD. Confirm the pin labels for your specific CYD revision before wiring.

The CYD touchscreen is not used by this firmware.
Music and Bluetooth
Place MP3 files in the music folder at the root of the Cardputer SD card. The Music Player reads from /sdcard/music and can play through the Cardputer speaker.

CYD Bluetooth Classic/A2DP output is under development. The firmware includes Bluetooth device scanning and connection controls, but the connection flow is not yet reliable. The Cardputer’s ESP32-S3 supports BLE, not Bluetooth Classic; use the CYD for Classic audio output when that feature is ready.
Building
The firmware uses ESP-IDF 5.x and keeps separate configuration files for the two boards:
- sdkconfig.cardputer for the Cardputer ADV (ESP32-S3)
- sdkconfig.cyd for the CYD (ESP32)
From the firmware project folder, build each target with its matching configuration:
idf.py -B ..\..\..\build-cardputer-clang -D SDKCONFIG=sdkconfig.cardputer build
idf.py -B build-cyd-clang2 -D SDKCONFIG=sdkconfig.cyd build
Each board must be flashed separately with the matching build and COM port. The Cardputer reads scripts and app state from its own SD card; the CYD does not access that card directly.
