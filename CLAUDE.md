# statusbar — Cutefish Status Bar

## Purpose
Top status bar showing time, system tray, battery, brightness, application menu (appmenu), power actions, and control center.

## Build
```bash
cmake -B build -DCMAKE_INSTALL_PREFIX=/usr && cmake --build build && sudo cmake --install build
```

## Dependencies
- Qt6 (Core, Widgets, DBus, Concurrent, Quick, QuickControls2, LinguistTools)
- KDE Frameworks 6 (KF6WindowSystem)

## Structure
- `src/main.cpp`, `src/statusbar.cpp/h` — main bar
- `src/controlcenterdialog.cpp/h` — control center
- `src/brightness.cpp/h`, `src/battery.cpp/h` — hardware indicators
- `src/appearance.cpp/h`, `src/notifications.cpp/h` — system features
- `src/processprovider.cpp/h`, `src/activity.cpp/h`, `src/capplications.cpp/h` — process tracking
- `src/poweractions.cpp/h` — power/shutdown actions
- `src/backgroundhelper.cpp/h` — background blur
- `src/systemtray/` — system tray (StatusNotifierItem/Watcher): 6 files
- `src/libdbusmenuqt/` — DBus menu import (from libdbusmenu-qt): 4 files
- `src/appmenu/` — global application menu: 12 files (appmenu model, importer, dbus adaptor)
- `src/volume.cpp/h` — volume control
- `qml/main.qml`, `qml/ControlCenter.qml`, `qml/SystemTray.qml`, `qml/ShutdownDialog.qml`, `qml/CardItem.qml`, `qml/StandardCard.qml`, `qml/StandardItem.qml`, `qml/IconButton.qml`, `qml/MprisItem.qml` — QML UI

### D-Bus Interfaces
- StatusNotifierWatcher, StatusNotifierItem
- DBusMenu
- AppMenu Registrar
- cutefish Statusbar

## Install Targets
- Binary → `${CMAKE_INSTALL_BINDIR}`
- Translations → `/usr/share/cutefish-statusbar/translations/`

## Qt5→Qt6 Migration Notes
- `cmake_minimum_version` 3.14 → 3.16
- C++11 → C++17
- Qt5 → Qt6, KF5WindowSystem → KF6WindowSystem
- Removed `Qt5::X11Extras` (replaced with `KF6::WindowSystem` + platform checks)

## Known Issues / Wayland Limitations
- App menu and active window tracking are X11-only (broken on Wayland)
- Needs layer-shell implementation for proper docking (currently uses X11 struts)
- System tray uses SNI (StatusNotifierItem) protocol via D-Bus — works on both X11 and Wayland

## Status
✅ Ported, built, installed, pushed (github.com/ali-soomro)
