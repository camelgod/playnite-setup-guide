# Game Streaming Setup Guide with Sunshine / Moonlight / Playnite

I wanted to simply boot up Moonlight and start playing any game I wanted using only a DS4 controller. I have no keyboard or mouse connected to my TV.

After lots of configuring and finding command line arguments and such, here is some knowledge that may or may not help you.

## My Setup

- [Sunshine](https://github.com/LizardByte/Sunshine)  (on a Windows 11 Desktop, Ethernet)
- [Moonlight](https://moonlight-stream.org/) (on a Nvidia Shield, Ethernet)
- [Playnite](https://github.com/JosefNemec/Playnite) (as the gallery / game launcher)
- Dualshock 4 (connected to the Nvidia Shield over bluetooth
- Switch Pro Controller (connected to the Nvidia Shield over bluetooth, used for Player 2 in co-op games)

## TODOS

I still havent figured out a way to consistently exit out of emulators. This will probably be updated in the future.

# Software Configuration

## 1. Install Playnite

Download and install Playnite on the host computer from the [releases page on github](https://github.com/JosefNemec/Playnite/releases)

## 2. Install Moonlight

Download and install Moonlight on your target (where you want to play the game)

Depending on your setup, Moonlight has alot of different clients. I use the app from Play Store on the shield - no sideloading or anything.

You can find the links to download on the [Moonlight Website](https://moonlight-stream.org/#)

## 3. Install Sunshine

Install [Sunshine](https://github.com/LizardByte/Sunshine/releases) on your host machine.

#### Add Playnite to Sunshine
To launch Playnite from Sunshine, click "Applications" up top menu and click "Add new".

Fill out the following (everything else is left as is or blank)

Application Name: `Playnite`

Command: `"C:\Users\YOURNAME\AppData\Local\Playnite\Playnite.FullscreenApp.exe" --hidesplashscreen`

Image: `C:\Users\YOURNAME\AppData\Local\Playnite\Themes\Fullscreen\Default\Images\applogo.png`



# Emulator Configuration

## Regarding RetroArch
[Retroarch](https://github.com/libretro/RetroArch) allows for quick install of a bunch of different emulators, Just open RetroArch, grab the cores you need, scan the Retroarch folder with Playnite and it will register the cores as emulators.

This allows you to set your settings inside Retroarch one time, and have it work across the cores.

Go to the Configure Emulators menu, open each retroarch profile, copy the original built-in arguments, and then check "Override Emulator Arguments", and add -f to each one in the beginning to launch them in fullscreen.

For example: `-f -L ".\cores\desmume_libretro.dll" "{ImagePath}"`

I have personally decided to move away from RetroArch, since many of the emulator cores are out of date or behave unexpectedly in regards to audio and video outputs. If it works fine for you its still a good pick for ease-of-use not having to set up a bunch of emulators manually.

## Manual Emulators

I have decided to move away from RetroArch, and set up everything manually. Below you will find a list of all the emulators I use and their respective launch arguments.


## Systems


### PC

Playnite can import your steam library, or manually import .exe

### Nintendo NES / Famicon

I use the **Mesen** emulator with the built-in arguments:

Built-in Arguments: `/fullscreen "{ImagePath}"`

### Nintendo SNES

I use the **snes9x** emulator with the built-in arguments:

Built-in Arguments: `"{ImagePath}" -fullscreen`

### Nintendo DS

I use the **DeSmuME** emulator with the built-in arguments.

I had a very hard time getting DeSmuMe fullscreen without using complicated AutoHotKey setups.
However I have a nifty trick up my sleeve using Playnite script to trigger ALT+Enter:

Go to DeSmuME in Emulator Configs and go to the "Scripts" tab. Execute after emulator is started paste the following:

`[System.Windows.Forms.SendKeys]::SendWait('%{ENTER}')`

In this case, `%` means hold ALT and `{ENTER}` is the Enter key.
![image](https://github.com/user-attachments/assets/75f619d5-371b-40e8-819c-4877384647ee)

This will open the emulator and then enter into fullscreen.

### Nintendo 3DS

I use the **Lime3DS* Emulator.

You have to add it as a custom emulator:

<img src="https://github.com/user-attachments/assets/3cbc1880-a3a2-47af-96f8-fc37321ff182" width="500">

You have two options for arguments:

**Windowed mode (GUI):**
1. Set the path to the `lime3ds-gui.exe`
2. Set the arguments to `"{ImagePath}"`

**Fullscreen mode (CLI):**
1. Set the path to the `lime3ds-cli.exe`
2. Arguments to `-f "{ImagePath}"`

I personally use the GUI executable and just set the Fullscreen. It will keep being fullscreen for future launches. I couldn't get the CLI version to launch without errors.

### Nintendo 64

I use the **Simple64** as described above.

Built-in Arguments: `--nogui "{ImagePath}"`

To get fullscreen on launch, there is no command-line and the Alt+Enter Script trick does not work for me.
You need to go and manually open Simple64, go to the option and enable fullscreen from there. Once enabled, it sticks on all future launches.

### Nintendo Gamecube

I use the **Dolphin** emulator with the default Built-in arguments.

Easiest way to launch with fullscreen is to open Dolphin and enable it.

### Nintendo Wii

I use the **Dolphin** emulator with the default Built-in arguments.

Easiest way to launch with fullscreen is to open Dolphin and enable it.

### Nintendo Switch

I use Ryujinx without overriding arguments in Playnite.

#### Issues
- There is no binding for exiting Ryujinx, or closing fullscreen with controller (which would let you use mouse simulation to close it).
- There is a feature request here: https://github.com/Ryujinx/Ryujinx/issues/3725 (It seems Ryujinx has been taken down)
- You can use one of these [Playnite recommended ways to closing a game](https://api.playnite.link/docs/manual/gettingStarted/helpAndTroubleshooting/faq.html#how-can-i-close-a-game-or-emulator-with-a-controller) but I personally don't like installing too much stuff.
- My solution: Don't use fullscreen, use mouse simulator to click the good old "X".

### PlayStation 1

I use the [DuckStation](https://github.com/stenzek/duckstation) emulator.

Using the built-in profile from PlayNite (`-batch -fullscreen "{ImagePath}"`)
### PlayStation 2

Install the [PCSX2]("https://github.com/PCSX2/pcsx2") manually.

Use custom arguments: `-batch -fullscreen -- {ImagePath}`

The batch argument will make PCSX2 close instantly when exiting the game.

Inside the PCSX2 Settings, I have set my touchpad clickdown (ps4 controller) to launch "Pause Menu", where I can exit the game to return to Playnite.

You can also set the "Exit Virtual Machine" to directly close the game.

### Sega Dreamcast

I use the **Flycast** Emulator with built-in launch arguments.

Easiest way is to open it, enable full-screen and it will stick in future sessions.

### PS Vita:

#### Set up Vita3k
When setting up Vita3k for the first time, you can select a folder other than AppData. I recommend using a new folder inside the emulator directory to make it more portable.

You don`t actually need to install this as an emulator inside Playnite.

1. Install the games through Vita3k
2. Take note of their install folder name (you can also right-click the games inside the emulator and click Open Folder - Application and take note of folder name)
3. Inside Playnite, Add a game Manually, import the metadata, and on the Action tab, use Vita3K.exe as path and add an argument `-r PCSE0443`

<img src="https://github.com/user-attachments/assets/f6df76f8-409e-4a94-8915-0a23b9741f77" width="500">





#### Issues:
- I can`t find a way to exit using your controller, which makes it hard to use for my controller-only setup.
    - This is why I don't use fullscreen arguments, since I rely on mouse emulation (hold Start button) and close it by clicking "X".
- Most games don't work properly in my experience



# List of emulator command line arguments

For some reason its really difficult to find full documentation of arguments for emulators. I've tried to collect them here.

## Lime3DS / Citra
I use Lime3DS, which is based on Citra.
I find the command line arguments to be the same.

From `lime3ds-cli.exe --help`:
```
Usage: lime3ds-cli.exe [options] <filename>
-g, --gdbport=NUMBER Enable gdb stub on port NUMBER
-i, --install=FILE    Installs a specified CIA file
-m, --multiplayer=nick:password@address:port Nickname, password, address and port for multiplayer
-r, --movie-record=[file]  Record a movie (game inputs) to the given file
-a, --movie-record-author=AUTHOR Sets the author of the movie to be recorded
-p, --movie-play=[file]    Playback the movie (game inputs) from the given file
-d, --dump-video=[file]    Dumps audio and video to the given video file
-f, --fullscreen     Start in fullscreen mode
-h, --help           Display this help and exit
-v, --version        Output version information and exit

```

## Simple64

Here are the command lines for Simple64-gui:
![image](https://github.com/user-attachments/assets/eaad9a07-8273-4ae9-b334-93b342f1abd8)



## Ryujinx

I have tried to decipher them from [here](https://github.com/Ryujinx/Ryujinx/blob/6ce49a2dc7b3e844b7152fa720a0bc30840f7609/src/Ryujinx.UI.Common/Helper/CommandLineState.cs#L29
). No guarantees!

```

-r, --root-data-dir     Not sure
-p, --profile           Path of the profile
-f, --fullscreen        Fullscreen Mode
-g, --graphics-backend  Change graphics backend
-i, --application-id    Launch Ryujinx with application ID
--docked-mode           Override Docked Mode
--handheld-mode         Override HandHeld Mode
--hide-cursor           Override Hide Cursor Setting
--software-gui          Override Hardware Acceleration for GUI

```

## DuckStation
Taken from the following link:

https://github.com/stenzek/duckstation/wiki/Command-Line-Arguments

```
Usage: duckstation-qt-x64-ReleaseLTCG.exe [parameters] [--] [boot filename]

  -help: Displays this information and exits.
  -version: Displays version information and exits.
  -batch: Enables batch mode (exits after powering off).
  -fastboot: Force fast boot for provided filename.
  -slowboot: Force slow boot for provided filename.
  -resume: Load resume save state. If a boot filename is provided,
    that game's resume state will be loaded, otherwise the most
    recent resume save state will be loaded.
  -state <index>: Loads specified save state by index. If a boot
    filename is provided, a per-game state will be loaded, otherwise
    a global state will be loaded.
  -statefile <filename>: Loads state from the specified filename.
    No boot filename is required with this option.
  -fullscreen: Enters fullscreen mode immediately after starting.
  -nofullscreen: Prevents fullscreen mode from triggering if enabled.
  -portable: Forces "portable mode", data in same directory.
  -nocontroller: Prevents the emulator from polling for controllers.
                 Try this option if you're having difficulties starting
                 the emulator.
  -settings <filename>: Loads a custom settings configuration from the
    specified filename. Default settings applied if file not found.
  --: Signals that no more arguments will follow and the remaining
    parameters make up the filename. Use when the filename contains
    spaces or starts with a dash.

```


## PCSX2 Command-Line Arguments

From here:

https://wiki.pcsx2.net/Command-line_support

```
 -help: Displays this information and exits.
 -version: Displays version information and exits.
 -batch: Enables batch mode (exits after shutting down).
 -nogui: Hides main window while running (implies batch mode).
 -elf <file>: Overrides the boot ELF with the specified filename.
 -disc <path>: Uses the specified host DVD drive as a source.
 -bios: Starts the BIOS (System Menu/OSDSYS).
 -fastboot: Force fast boot for provided filename.
 -slowboot: Force slow boot for provided filename.
 -state <index>: Loads specified save state by index.
 -statefile <filename>: Loads state from the specified filename.
 -fullscreen: Enters fullscreen mode immediately after starting.
 -nofullscreen: Prevents fullscreen mode from triggering if enabled.
 -bigpicture: Forces PCSX2 to use the Big Picture mode (useful for controller-only and couch play).
 -gameargs="-arg1 -arg2": Supplies launch arguments to the game itself ("-arg1" and "-arg2" will be passed to the game in this example).
 --: Signals that no more arguments will follow and the remaining
   parameters make up the filename. Use when the filename contains
   spaces or starts with a dash.
```

## Flycast

Flycast Command Line Arguments need to be passed through a `-config` flag.

For example: `-config  section:key=value`

With real data: `-config window:fullscreen=yes`

For detailed information see the Flycast Wiki:
https://github.com/TheArcadeStriker/flycast-wiki/wiki/Configuration-files-and-command-line-parameters#command-line-parameters


## Vita3K Command Line Interface

From the `Vita3K.exe --help` output.

```
Vita3K Command Line Interface
Usage: C:\Path\Vita3K.exe [OPTIONS] [content-path]

Positionals:
  content-path TEXT                   Path to the app with a .vpk/.zip extension or folder of content to install & run

Options:
  -h,--help                           Print this help message and exit
  -v,--version                        Print the version string
[Option Group: Input]
  Special options for Vita3K
  Options:
    --firmware TEXT                     Path to the firmware file (.pup extension) to install

  Input:
    -z,--console [0]                    Start the emulator in console mode.
    -Z,--app-args TEXT                  Argument for app, use ', ' to separate arguments.
    -a,--load-app-list BOOLEAN [0]      Starts the emulator with load app list.
    -S,--self TEXT [eboot.bin]          Path to the self to run inside Title ID
    -r,--installed-path TEXT:{PCSA00099,PCSA00152,PCSB00291,PCSB00346,PCSB00404,PCSE00240,PCSE00443,PCSE00508,PCSE00644,PCSG00205}
                                        Path to the installed app to run
    -s,--recompile-shader TEXT          Recompile the given PS Vita shader (GXP format) to SPIR_V / GLSL and quit
    -d,--deleted-id TEXT:{PCSA00099,PCSA00152,PCSB00291,PCSB00346,PCSB00404,PCSE00240,PCSE00443,PCSE00508,PCSE00644,PCSG00205}
                                        Title ID of installed app to delete
    --pkg TEXT Needs: --zrif            Path to the app file (.pkg extension) to install
    --zrif TEXT Needs: --pkg            zrif to decode the app (base64 format)
[Option Group: Configuration]
  Modify Vita3K's config.yml file
  Logging:
    -A,--archive-log                    Make a duplicate of the log file with TITLE_ID and Game ID as title
    -l,--log-level INT:INT in [0 - 6]   Logging level:
                                        TRACE = 0
                                        DEBUG = 1
                                        INFO = 2
                                        WARN = 3
                                        ERROR = 4
                                        CRITICAL = 5
                                        OFF = 6
    -S,--log-active-shaders             Log Active Shaders
    -U,--log-uniforms                   Log Uniforms

  Vita Emulation:
    -B,--backend-renderer TEXT:{OpenGL,Vulkan}
                                        Renderer backend to use
    -C,--color-surface-debug            Save color surfaces

  YML:
    -c,--config-location TEXT           Get a configuration file from a given location. If a filename is given, it must end with ".yml", otherwise it will be assumed to be a directory.
                                        Default loaded: <Vita3K>/config.yml
                                        Defaults: <Vita3K>/data/config/default.yml
    -w{false},--keep-config{false}      Do not modify the configuration file after loading.
    -f,--load-config                    Load a configuration file. Setting --keep-config with this option preserves the configuration file.
    -F,--fullscreen                     Start the emulator in fullscreen mode.

  Modules:
    -m,--lle-modules TEXT ...           Load given (decrypted) OS modules from disk.
                                        Separate by commas to specify multiple modules. Full path and extension should not be included, the following are assumed: vs0:sys/external/<name>.suprx
                                        Example: --lle-modules libscemp4,libngs

```


## Dolphin

Command Line Options from their wiki: https://wiki.dolphin-emu.org/index.php?title=Help:Contents

```
-h, --help                                    Show this help message
-d, --debugger                                Opens the debugger
-l, --logger                                  Opens the logger
-e, --exec=<str>                              Loads a specific game file (ELF, DOL, GCM, ISO, WBFS, CISO, GCZ, WAD)
-n, --nand_title=<str>                        Launch a NAND title
-b, --batch                                   Exit Dolphin with emulator
-c, --confirm                                 Set "Confirm on Stop".
-v, --video_backend=<str>                     Specifies a video backend to use, D3D or OGL.
-a, --audio_emulation=<str>                   Specified the type of audio to use, HLE or LLE.
-m, --movie=<str>                             Plays a movie file
-u, --user=<str>                              Specifies a path to the user directory
-C, --config=<System>.<Section>.<Key>=<Value> Set a configuration option.

```

## RetroArch

Retro Arch will basically use its own command line arguments to run the core.

```
Usage: C:\path\retroarch.exe [OPTIONS]... [FILE]

  -h, --help                     Show this help message.
  -v, --verbose                  Verbose logging.
      --log-file=FILE            Log messages to FILE.
  -V, --version                  Show version.
      --features                 Print available features compiled into program.
      --menu                     Do not require content or libretro core to be loaded,
                                   starts directly in menu. If no arguments are passed to
                                   the program, it is equivalent to using --menu as only argument.
  -c, --config=FILE              Path for config file.
                                   Defaults to retroarch.cfg in same directory as retroarch.exe.
                                   If a default config is not found, the program will attempt to create one.
      --appendconfig=FILE        Extra config files are loaded in, and take priority over
                                   config selected in -c (or default). Multiple configs are
                                   delimited by '|'.
  -L, --libretro=FILE            Path to libretro implementation. Overrides any config setting.
                                   FILE may be one of the following:
                                   1. The full path to a core shared object library: path/to/<core_name>_libretro.<lib_ext>
                                   2. A core shared object library 'file name' (*): <core_name>_libretro.<lib_ext>
                                   3. A core 'short name' (*): <core_name>_libretro OR <core_name>
                                   (*) If 'file name' or 'short name' do not correspond to an existing full file path,
                                   the configured frontend 'cores' directory will be searched for a match.
      --subsystem=NAME           Use a subsystem of the libretro core. Multiple content
                                   files are loaded as multiple arguments. If a content
                                   file is skipped, use a blank ("") command line argument.
                                   Content must be loaded in an order which depends on the
                                   particular subsystem used. See verbose log output to learn
                                   how a particular subsystem wants content to be loaded.
      --scan=PATH|FILE           Import content from path.
  -f, --fullscreen               Start the program in fullscreen regardless of config setting.
      --set-shader=PATH          Path to a shader (preset) that will be loaded each time content is loaded.
                                   Effectively overrides automatic shader presets.
                                   An empty argument "" will disable automatic shader presets.
  -N, --nodevice=PORT            Disconnects controller device connected to PORT (1 to 16).
  -A, --dualanalog=PORT          Connect a DualAnalog controller to PORT (1 to 16).
  -d, --device=PORT:ID           Connect a generic device into PORT of the device (1 to 16).
                                   Format is PORT:ID, where ID is a number corresponding to the particular device.
  -M, --sram-mode=MODE           SRAM handling mode. MODE can be:
                                   'noload-nosave', 'noload-save', 'load-nosave' or 'load-save'.
                                   Note: 'noload-save' implies that save files *WILL BE OVERWRITTEN*.
  -H, --host                     Host netplay as user 1.
  -C, --connect=HOST             Connect to netplay server as user 2.
      --port=PORT                Port used to netplay. Default is 55435.
      --mitm-session=ID           MITM (relay) session ID to join.
      --nick=NICK                Picks a username (for use with netplay). Not mandatory.
      --check-frames=NUMBER      Check frames when using netplay.
      --command                  Sends a command over UDP to an already running program process.
                                   Available commands are listed if command is invalid.
  -P, --play-replay=FILE         Playback a replay file.
  -R, --record-replay=FILE       Start recording a replay file from the beginning.
      --eof-exit                 Exit upon reaching the end of the replay file.
  -r, --record=FILE              Path to record video file. Using mkv extension is recommended.
      --recordconfig             Path to settings used during recording.
      --size=WIDTHxHEIGHT        Overrides output video size when recording.
  -D, --detach                   Detach program from the running console. Not relevant for all platforms.
      --max-frames=NUMBER        Runs for the specified number of frames, then exits.
  -U, --ups=FILE                 Specifies path for UPS patch that will be applied to content.
      --bps=FILE                 Specifies path for BPS patch that will be applied to content.
      --ips=FILE                 Specifies path for IPS patch that will be applied to content.
      --xdelta=FILE              Specifies path for Xdelta patch that will be applied to content.
      --no-patch                 Disables all forms of content patching.
      --max-frames-ss            Takes a screenshot at the end of max-frames.
      --max-frames-ss-path=FILE  Path to save the screenshot to at the end of max-frames.
      --accessibility            Enables accessibilty for blind users using text-to-speech.
      --load-menu-on-error       Open menu instead of quitting if specified core or content fails to load.
  -e, --entryslot=NUMBER         Slot from which to load an entry state.
  -s, --save=PATH                Path for save files (*.srm). (DEPRECATED, use --appendconfig and savefile_directory)
  -S, --savestate=PATH           Path for the save state files (*.state). (DEPRECATED, use --appendconfig and savestate_directory)

```
