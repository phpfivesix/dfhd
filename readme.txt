==========================================================
 DELTA FORCE 1 (1998) HD  --  v1.00.04.00
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
- Resolutions above 1024x768 are available, up to the
  desktop resolution. The HUD scales accordingly.
- Windowed mode works, including mouse-look
  (dfhd.cfg: windowed = 1).
- Satchel charges and claymores work again in single
  player (broken in stock 3.03).
- Jump key presses register reliably (the original engine
  dropped roughly half of short taps).
- Distant objects no longer render white or through the
  terrain beyond 512 m.
- The renderer is the original software renderer. High
  resolutions are CPU-heavy; single-core speed matters.
- The terrain renderer can use multiple CPU cores (on by
  default, see Shift+H below).
- Optional higher terrain and model detail, and a fix for
  the terrain "popping" while looking up and down at high
  resolutions (see COMMANDS below).
- F12 (letterbox size) has two extra steps: full screen
  with the HUD, and full screen without the HUD.

MULTIPLAYER
-----------
- The network send rate can be set by hand (mp_tickrate),
  and remote players can be smoothed at low send rates
  (mp_interpolate). See COMMANDS below.
- Joining a game no longer hangs forever: searching for and
  connecting to a server shows a status line and gives up
  after a timeout, returning to the menu.
- The Host menu no longer shows "your IP address is" (on
  machines with several network adapters or a VPN it often
  showed the wrong address).
- The NovaWorld server listing uses a master server, set
  in dfhd.cfg (multiplayer section):
      master_server = "host:port"      (or "ip:port")
  ":port" is optional (default 3875); blank = no master.
  The listing announce carries the game GUID and version.
  The stock 208.231.90.229 master is long dead; leave this
  blank unless you run your own.
- The MultiPlayer "NovaWorld" page's "default browser"
  button now works: set dfhd.cfg master_server_list to your
  server-list web page URL and it opens in your default
  browser. Blank falls back to the local Browser.htm.
- The "mini browser" option (novawrld.exe) follows the same
  master_server_list URL: it always loads the local
  Startup.htm, so the game rewrites that file's redirect to
  your URL before launching it. Blank leaves Startup.htm as
  shipped.

KEY SHORTCUTS
-------------
V         cycle the resolution, through all available
          modes including the high resolutions up to
          the desktop size
Shift+V   cycle display scale mode
          (integer / fit / stretch / unscaled;
          saved as dfhd.cfg scale_mode)
Shift+H   toggle the multithreaded terrain renderer
          (saved as dfhd.cfg terrain_mt)
Shift+;   toggle the FPS overlay
F12       letterbox size, now 4 steps: small bars /
          large bars / full screen + HUD /
          full screen without HUD

COMMANDS
--------
Open the console with the ` (~) key and type a command.
Settings marked [cfg] are saved in dfhd.cfg.

showfps                toggle the FPS overlay (Shift+;)
scalemode              cycle the display scale mode
                       (Shift+V)                    [cfg]
terrain_mt             toggle the multithreaded terrain
                       renderer (Shift+H)           [cfg]
terrain_lod 0..4       distant terrain detail;
                       0 = original, 4 = highest    [cfg]
model_lod 0..4         distance at which models keep
                       their detail;
                       0 = original, 4 = highest    [cfg]
terrain_precision 0|1  1 = fix the terrain "popping"
                       while looking up/down at high
                       resolutions; 0 = original    [cfg]
mp_tickrate [n]        multiplayer send interval in game
                       ticks (send rate ~62/n Hz):
                       1 = fastest (~62 Hz), 6 = LAN
                       preset (~10 Hz), 0 = automatic
                       (follow the connection type).
                       Without a value it shows the
                       current rate and the choices. [cfg]
mp_interpolate         toggle smoothing of remote players
                       between network updates; helps at
                       low send rates. Default off. [cfg]

terrain_lod, model_lod and terrain_precision can also be
set on the command line, e.g.
    dfhd.exe -terrain_lod 4 -model_lod 4 -terrain_precision 1

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
