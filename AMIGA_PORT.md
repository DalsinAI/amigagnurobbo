GNU Robbo 0.68 for AmigaOS 3.x
==============================

GNU Robbo (the GNU Robbo Team, http://gnurobbo.sourceforge.net), the
logic game after Janusz Pelc's Robbo for the Atari XL/XE: guide the little
robot through each planet's maze, collect the screws and the capsule's
parts, and get away. Hundreds of levels, three skins and a level designer.
For AmigaOS 3.x on a 68040 or 68060 with an FPU and an RTG screen, on
OpenGPU's SDL 1.2 (sdl12-compat).

Base: gnurobbo_0.68+dfsg.orig.tar.bz2 from Debian (sha256
5a542aa210744ec600b232b02fdd1b7f8b03684f8ad92e1d48d8d0a32bbf69d6):
upstream's 0.68 without its sounds, music and font (and their own licence
files), which Debian leaves out of its free source. Debian's patches (0.68+dfsg-6: format-security,
reproducible-build, gcc-7, single-variable-declarations) are the second
commit. Branch team2/gnurobbo-amiga.

Status: builds; not yet run in the lab.


What you need
-------------

- A 68040 or 68060 with an FPU, AmigaOS 3.x, an RTG card (or the
  AmigaChrome lab).
- GFOpenUp 0.8.18 or later (LIBS:OpenGPU/SDL2.module). Everything else is
  in the program.


How to play
-----------

Open the GNURobbo icon, or run GNURobbo from a Shell. The game reads its
levels, skins and translations from the drawer's data/ and keeps its
settings and your own levels in user/. Like Debian's package, it has no
sound: the source it is built from has none.


Building
--------

    make -f amiga/Makefile.amigaos -j2 dist

with GFOpenAmigaGCC 16.2.0-open4, the OpenNDK headers, the OpenGPU kit and
the Team's static FreeType, libpng, zlib and bzip2 (see the Makefile's
head). The drawer is dist/GNURobbo (and dist/GNURobbo.info).


What was changed
----------------

- No source change beyond Debian's patches. amiga/Makefile.amigaos builds
  upstream's PC configuration (designer, smooth scrolling, lightning, the
  SDL_ttf font) without music, with PACKAGE_DATA_DIR = PROGDIR:data.
- amiga/amiga_env.c (-Wl,--wrap=getenv): $HOME is the drawer's user/
  (made at the first start), where the game keeps .gnurobbo_rc and
  .gnurobbo/levels.
- Each skin's robbo.ttf is DejaVu Sans (Debian links a DejaVu font there:
  the original font is not in the source).
- No SDL_image, SDL_mixer or SDL_ttf 1.2 for OpenGPU's SDL 1.2: the Team's
  amiga/sdl_image_lite.c (PNG), amiga/sdl_mixer_lite.c and SDL_ttf 2.0.11
  (amiga/sdl_ttf, zlib licence) stand in, as in the Hex-a-hop port.
  SDL_RWFromFile is stdio (amiga/amiga_rwops.c).
- amiga/stack.c: 512 KB of stack.


Licences
--------

GNU Robbo and its levels and pictures: GPL 2 or later (COPYING.txt).
DejaVu Sans: data/skins/DejaVu-LICENSE.txt. SDL_ttf 2.0.11: zlib
(SDL_ttf-COPYING.txt). The Amiga files (amiga/): the AmiCradle Team; the
SDL_image, SDL_mixer and rwops shims come from the Team's Wizznic and
Gigalomania ports and are GPL 3 or later, so the program as built here is
GPL 3 or later.
