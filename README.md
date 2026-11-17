# 86Box-PZVM

A modified build of [86Box](https://github.com/86Box/86Box) for PZVM, a Project Zomboid
mod that runs virtual machines on in-game computers and shows them over VNC.

This is not an official 86Box release and is not supported by the 86Box team. Please
report problems with this build here, not to the 86Box project.

## What is different

The VNC renderer is made usable for running several headless machines from another
program: a port per VM, loopback-only listening, a hidden main window, mouse input
without host mouse capture, and resolution changes sent to VNC clients. All changes,
the new `86box.cfg` settings and the Windows build steps are in [PZVM.md](PZVM.md).

## Credits and licence

86Box is written by the 86Box team and contributors (see [AUTHORS](AUTHORS)). This fork
and its changes are released under the GNU General Public License, version 2 or later,
like 86Box itself. See [COPYING](COPYING).

86Box can optionally use [munt](https://github.com/munt/munt),
[FluidSynth](https://www.fluidsynth.org/) and [Ghostscript](https://www.ghostscript.com/),
which are distributed under their own licences.

The ROM set 86Box needs to run is not part of this repository.
