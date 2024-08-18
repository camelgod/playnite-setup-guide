# Game Streaming Setup Guide with Sunshine / Moonlight / Playnite

I wanted to simply boot up Moonlight and start playing any game I wanted using only a DS4 controller. I have no keyboard or mouse connected to my TV.

After lots of configuring and finding command line arguments and such, here is some knowledge that may or may not help you.

## My Setup

- [Sunshine](https://github.com/LizardByte/Sunshine)  (on a Windows 11 Desktop, Ethernet)
- [Moonlight](https://moonlight-stream.org/) (on a Nvidia Shield, Ethernet)
- [Playnite](https://github.com/JosefNemec/Playnite) (as the gallery / game launcher)
- Dualshock 4 (connected to the Nvidia Shield over bluetooth)

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

[Retroarch](https://github.com/libretro/RetroArch) allows for quick install of a bunch of different emulators, Just open RetroArch, grab the cores you need, scan the Retroarch folder with Playnite and it will register the cores as emulators.

This allows you to set your settings inside Retroarch one time, and have it work across the cores.

Go to the Configure Emulators menu, open each retroarch profile, copy the original built-in arguments, and then check "Override Emulator Arguments", and add -f to each one in the beginning to launch them in fullscreen.

I don't recommend the PCSX2 and PCX core in Retroarch. I use the standalone PCSX2, Vita3k, DuckStation and Ryujinx emulators.

RetroArch has some audio issues for me on Windows 11, so I'm in the process of moving to 100% stand-alone emulator setup.

## Systems


### PC

Playnite can import your steam library, or manually import .exe

### Nintendo NES / Famicon

I use the RetroArch core **Nestopia** as described above.

Custom Arguments: `-f -L ".\cores\nestopia_libretro.dll" "{ImagePath}"`

### Nintendo SNES

I use the RetroArch core **snes9x** as described above.

Custom Arguments: `-f -L ".\cores\snes9x_libretro.dll" "{ImagePath}"`

### Nintendo DS

I use the RetroArch core **DeSmuME** as described above.

Custom Arguments: `-f -L ".\cores\desmume_libretro.dll" "{ImagePath}"`

### Nintendo 3DS

I use the Lime3DS Emulator.

You have to add it as a custom emulator:
![image](https://github.com/user-attachments/assets/3cbc1880-a3a2-47af-96f8-fc37321ff182)

You have two options for arguments:

**Windowed mode (GUI):**
1. Set the path to the `lime3ds-gui.exe`
2. Set the arguments to `"{ImagePath}"`

**Fullscreen mode (CLI):**
1. Set the path to the `lime3ds-cli.exe`
2. Arguments to `-f "{ImagePath}"`


### Nintendo 64

I use the RetroArch core **Mupen64Plus-next** as described above.

Custom Arguments: `-f -L ".\cores\mupen64plus_next_libretro.dll" "{ImagePath}"`

### Nintendo Gamecube

I use the RetroArch core **Dolphin** as described above.

Custom Arguments: `-f -L ".\cores\dolphin_libretro.dll" "{ImagePath}"`

### Nintendo Wii

I use the RetroArch core **Dolphin** as described above.

Custom Arguments: `-f -L ".\cores\dolphin_libretro.dll" "{ImagePath}"`

### Nintendo Switch

I use Ryujinx without overriding arguments in Playnite.

#### Issues
- There is no binding for exiting Ryujinx, or closing fullscreen with controller (which would let you use mouse simulation to close it).
- There is a feature request here: https://github.com/Ryujinx/Ryujinx/issues/3725
- You can use one of these [Playnite recommended ways to closing a game](https://api.playnite.link/docs/manual/gettingStarted/helpAndTroubleshooting/faq.html#how-can-i-close-a-game-or-emulator-with-a-controller) but I personally don't like installing too much stuff.
- My solution: Don't use fullscreen, use mouse simulator to click the "X".

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

I use the RetroArch core **Flycast**

Use custom arguments `-f -L ".\cores\flycast_libretro.dll" "{ImagePath}"`

### PS Vita:

#### Set up Vita3k
When setting up Vita3k for the first time, you can select a folder other than AppData. I recommend using a new folder inside the emulator directory to make it more portable.

You don`t actually need to install this as an emulator inside Playnite.

1. Install the games through Vita3k
2. Take note of their install folder name (you can also right-click the games inside the emulator and click Open Folder - Application and take note of folder name)
3. Inside Playnite, Add a game Manually, import the metadata, and on the Action tab, use Vita3K.exe as path and add an argument `-r PCSE0443`

#### Issues:
- I can`t find a way to exit using your controller, which makes it hard to use for my controller-only setup.
    - This is why I don't use fullscreen arguments, since I rely on mouse emulation (hold Start button) and close it by clicking "X".
- Most games don't work properly in my experience



# List of emulator command line arguments

For some reason its really difficult to find full documentation of arguments for emulators.

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



