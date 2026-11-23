==========================================================
 DELTA FORCE 1 (1998) HD  --  v1.00.04.03
 based on Delta Force v1.00.03.03P (NovaLogic, 1998)
==========================================================

An updated game executable (dfhd.exe) for Delta Force.
Game data, missions and gameplay are unchanged unless
listed below.

INSTALLATION
------------
1. Copy dfhd.exe into an existing Delta Force v3.03
   installation directory. It does not replace or touch
   the original Df.exe.
2. Run dfhd.exe from that directory. Its settings are kept
   in dfhd.cfg (the original df.cfg is left alone); player
   profiles (player*.ply) are shared with the original.

WINDOWS SMARTSCREEN
-------------------
dfhd.exe is not code-signed, so the first time you run it
Windows may show "Windows protected your PC":
  - Click "More info", then "Run anyway".
If the file came from a download or a zip and Windows
blocks it outright:
  - Right-click dfhd.exe > Properties, tick "Unblock" at
    the bottom of the General tab, click OK, and run it
    again.
  (When the zip itself is unblocked the same way before
  extracting, every file in it is unblocked.)

GENERAL
-------
- Full GPU rendering, with an optional mesh terrain with
  a voxel look.
- Added 32-player multiplayer support.
- Resolutions above 1024x768 are available, up to the
  desktop resolution. The HUD scales accordingly.
- Windowed mode works, including mouse-look.
- Satchel charges and claymores work again in single
  player (broken in stock 3.03).
- Jump key presses register reliably (the original engine
  dropped roughly half of short taps).
- Distant objects no longer render white or through the
  terrain beyond 512 m.
- F12 (letterbox size) has two extra steps: full screen
  with the HUD, and full screen without the HUD.
- Single player has a new in-game menu to change the
  graphics settings.

SETTINGS
--------
- The main menu's Settings button opens two new pages,
  General and Graphics.
- General: added scope sensitivity and an optional
  update check.
- Graphics: use Scale Filter "Sharp Bilinear" for display
  resolutions the menus and text can't scale to evenly.
  This fixes the text rendering without making it blurry.
- Graphics: choose the original software-rendered voxel
  terrain (multicore), the voxel terrain as a hardware
  shader, or a mesh terrain with a voxel look.

GRAPHICS DRIVER
---------------
Settings > Graphics > Driver: Auto, Direct3D 12, Vulkan
or Direct3D 11. Auto uses Direct3D 12, and Direct3D 11
when Direct3D 12 can't start.

On older graphics cards, or when the game crashes or
draws wrong, choose Direct3D 11. If the game does not
start at all, open dfhd.cfg (next to dfhd.exe) in Notepad
and change the display_driver line to:
    display_driver              = direct3d11

No dfhd.cfg yet? Create it with these two lines (without
the first one the game resets the file):
    update_check_url = "https://api.github.com/repos/phpfivesix/dfhd/releases/latest"
    display_driver = direct3d11

UPDATE CHECK
------------
- The game has an optional update check. Nothing is
  downloaded automatically: the version button in the
  menu links to the GitHub releases page, where you can
  download the new version yourself.

MULTIPLAYER
-----------
- Simple prediction and smoothing added. See COMMANDS.
- Players with a slow send rate should no longer drop
  shots.
- The network send rate can be set by hand (mp_tickrate).
  Host and clients can move jumping players smoothly
  between their updates (mp_predict), and soften
  the jumps of other players' network corrections
  (mp_smooth). See COMMANDS below.
- Connection Type offers LAN, Internet and NovaWorld.
  Modem and Serial are gone, and with them DirectPlay.
- The NovaWorld server listing uses a master server, set
  in dfhd.cfg (multiplayer section):
      master_server = "host:port"      (or "ip:port")
  ":port" is optional (default 3875); blank = no master.
  The listing announce carries the game GUID and version.
  The stock 208.231.90.229 master is long dead; leave this
  blank unless you run your own.
- The link on the MultiPlayer "NovaWorld" page can be set
  in dfhd.cfg (master_server_list) to your server-list
  web page; it opens in your default browser. Blank falls
  back to the local Browser.htm.

PORTS AND ROUTERS
-----------------
- Added server port settings to the menu: host on a
  custom port, or join a server on a custom port.
- The server answers the port the client sends from, no
  longer the hard-coded port 3568.

Joining from behind a router:
    you run    the host runs   forward on your router
    dfhd.exe   dfhd.exe        nothing
    dfhd.exe   Df.exe          UDP 3568 to your PC
    Df.exe     either          UDP 3568 to your PC

DEDICATED SERVER
----------------
The game can now run as a dedicated server, with no
window, no sound and no menus:
    dfhd.exe -dedicated -platform null

It hosts with the multiplayer settings of the dfhd.cfg in
its folder (read-only). Give the server its own folder
(the game files plus dfhd.exe and a dfhd.cfg) when you
also play from the same PC.
- -dedicated     host at once, no menus
- -platform null no window, no input, no sound device
                 (without it the server keeps a window)

dfhd.cfg keys the server uses:
    mp_service    1 (Internet/LAN) or 4 (NovaWorld)
    mp_gametype   1..5 (the Host menu's game types)
    replay        0 one game, then the server stops;
                  1 the same map again;
                  2 the next map
    dedicated_rotation = "C08M01 C08M17 C08M08"
                  the maps' type must match mp_gametype

Server console commands:
    players        the player list
    quit (or exit) stop the server

Ctrl + C, Ctrl + Break and closing the console also stop
the server.

The server's profile is server.ply in its folder.

LOGS AND CRASHES
----------------
Each start writes dfhd_log_last_run.txt next to dfhd.exe.
A crash writes dfhd_crashlog_<date>_<time>.txt, plus
SYSDUMP.TXT and MEMDUMP.TXT. Send these files with a bug
report.

Command line log options:
-log 1..3         log verbosity
-log_net 1        the network layer's lines in
                  netsock.log as well
-log_file <name>  the log under another name

KEY SHORTCUTS
-------------
V           cycle the resolution, through all available
            modes including the high resolutions up to
            the desktop size
Shift + V   cycle the display scale mode
            (integer / fit / stretch / unscaled)
Ctrl + V    switch the world renderer between soft and GPU
Shift + H   toggle the multithreaded terrain renderer
Shift + ;   toggle the FPS overlay
F12         letterbox size, now 4 steps: small bars /
            large bars / full screen + HUD /
            full screen without HUD

COMMANDS
--------
Open the console with the ` (~) key and type a command.
Settings marked [cfg] are saved in dfhd.cfg.

showfps                toggle the FPS overlay (Shift + ;)
scalemode              cycle the display scale mode
                       (Shift + V)                  [cfg]

mp_tickrate [n]        send interval in game ticks
                       (~62/n Hz): 1 = fastest, 6 = LAN,
                       0 = auto (by connection type).
                       Without a value it shows the
                       current rate.                [cfg]
mp_predict n           1 = other players keep moving
                       through a jump between updates.
                       Default 0.                   [cfg]
mp_relay_budget n      on a host: players a client
                       hears of per send, 1..31
                       (0 = the original's 15). With
                       more than 16 players, 31 keeps
                       them smooth for twice the
                       upload. Default 0.           [cfg]
mp_smooth n            1 = other players glide to a
                       corrected position instead of
                       jumping. Default 0.          [cfg]

New cheats (single player only, typed in the console like
the original cheats):

freecam                detach the camera from the player
                       and fly around: W/S forward/back
                       along the view, A/D strafe,
                       mouse/arrows look, Space/Q up/down,
                       Shift 4x speed. Type again (or
                       start a mission) to return.
isaidthelimit          weapons fire without refire or
                       reload delay. Needs the
                       takeittothelimit cheat (infinite
                       ammo) to be on first.
timescale n            the mission's speed in percent,
                       10 to 200: 25 is slow motion at a
                       quarter speed, 200 double speed.
                       Sound keeps its normal speed.

DEFAULT KEYS
------------
Newly created soldiers use the layout below. Existing
profiles keep their saved bindings; open the keyboard
settings and use "Restore Defaults" to switch. All keys
are rebindable in-game.

  W / S          forward / back
  A / D          strafe left / right
  Space          jump
  Z / X / C      prone / stand / crouch
  Shift          walk
  H              turbo
  Arrow keys     turn / look

  Mouse 1, Ctrl  fire
  Mouse 2        scope
  Mouse 3        prone
  R              reload
  Q              next weapon
  1 .. 0         weapon slots
  + / -          zoom in / out
  B              binoculars

  T / Y          chat / team chat
  M              map
  Tab            next observer target (in F9 view)
  , / .          previous / next waypoint
  J              next flag
  O              mission briefing
  G              mission goals
  I              recent messages
  N              show friendly names
  U              audio macros
  Del            drop
  V              cycle resolution
  Home           server screen
  `              console

CREDITS
-------
dfhd.exe contains SDL 3 (Simple DirectMedia Layer,
https://www.libsdl.org), statically linked, under the zlib
license: Copyright (C) 1997-2026 Sam Lantinga.
