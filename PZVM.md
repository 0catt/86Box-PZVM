# 86Box for PZVM

This is a modified build of [86Box](https://github.com/86Box/86Box) used by PZVM, a
Project Zomboid mod that shows virtual machines on in-game computers over VNC. It is not
an official 86Box release and is not supported by the 86Box team.

86Box is licensed under the GNU General Public License, version 2 or later (see
`COPYING`). These changes are under the same licence.

## Changes

All changes are on the `pzvm-vnc` branch. Each changed file carries a
"Modified for PZVM" line with the date.

New settings in the `[General]` section of a VM's `86box.cfg`, used with
`vid_renderer = vnc`:

| Setting | Default | Meaning |
|---|---|---|
| `vnc_port` | `5900` | TCP port of the VNC server, for IPv4 and IPv6 |
| `vnc_local_only` | `0` | `1` listens on 127.0.0.1 and ::1 only |
| `vnc_hide_window` | `0` | `1` never shows the main window |

The VNC renderer also sets `mouse_automation` while it is active, so the emulated
mouse accepts VNC pointer input without the (hidden) window capturing the host mouse.
Upstream 86Box drops VNC mouse input unless the window has captured the mouse.

Build changes:

- `qt_downloader.cpp` is only built together with the update checker, so builds
  without the update checker do not link Qt's SSL support or OpenSSL.
- Static FluidSynth builds no longer link GNU readline and termcap. FluidSynth only
  uses them for its command shell, which 86Box never opens; `midi_fluidsynth.c`
  provides empty stand-ins for `readline` and `add_history`.

## Building on Windows

1. Install [MSYS2](https://www.msys2.org/) and open the UCRT64 shell.
2. Install the packages:

   ```sh
   pacman -S --needed $MINGW_PACKAGE_PREFIX-{ninja,cmake,gcc,pkgconf,openal,freetype,sdl3,zlib,zstd,libpng,rtmidi,fluidsynth,libslirp,libsndfile,qt5-static,qt5-translations,vulkan-headers,libvncserver}
   ```

3. Configure and build:

   ```sh
   cmake -G Ninja -B build -S . --preset regular -D VNC=ON -D DISCORD=OFF
   cmake --build build
   ```

The exe is `build/src/86Box.exe`. It needs `libvncserver.dll` and its dependencies
from `/ucrt64/bin` next to it, and the 86Box ROM set, which is not part of this
repository.
