# Comfy Game Streaming Setup Guide with Sunshine / Moonlight / Playnite

I wanted to simply boot up Moonlight and start playing any game I wanted using only a DS4 controller. I have no keyboard or mouse connected to my TV.

After lots of configuring and finding command line arguments and such, here is some knowledge that may or may not help you.

## My Setup
My setup is as follows:
- [Sunshine](https://github.com/LizardByte/Sunshine)  (on a Windows 11 Desktop, Ethernet)
- [Moonlight](https://moonlight-stream.org/) (on a Nvidia Shield, Ethernet)
- [Playnite](https://github.com/JosefNemec/Playnite) (as the gallery / game launcher)
- Dualshock 4 (connected to the Nvidia Shield over bluetooth)

# 1. Software Configuration

## Add Playnite as an Application inside Sunshine

To launch Playnite from Sunshine, click "Applications" up top menu and click "Add new".

Fill out the following (everything else is left as is or blank)

Application Name: `Playnite`

Command: `"C:\Users\YOURNAME\AppData\Local\Playnite\Playnite.FullscreenApp.exe" --hidesplashscreen`

Image: `C:\Users\YOURNAME\AppData\Local\Playnite\Themes\Fullscreen\Default\Images\applogo.png`



# 2. Emulator Configuration

The fastest way to get set up is to install [Retroarch](https://github.com/libretro/RetroArch) and just grab the cores, scan the Retroarch folder with Playnite and it will register the cores as emulators.

This allows you to set your settings inside Retroarch one time, and have it work across the cores.

Go to the Configure Emulators menu, open each retroarch profile, copy the original built-in arguments, and then check "Override Emulator Arguments", and add -f to each one in the beginning to launch them in fullscreen.


## Systems


### PC

Playnite can import your steam library
Manually import the .exe

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

I use the RetroArch core **Citra** (NOT the 2018) as described above

Custom Arguments: `-f -L ".\cores\citra_libretro.dll" "{ImagePath}"`

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

I use Ryujinx without overriding arguments.
Instead, Ive set the config inside Ryujinx.

### PlayStation 1

I use the RetroArch core **PCSX Rearmed** as described above

Custom Arguments: `-f -L ".\cores\pcsx_rearmed_libretro.dll" "{ImagePath}"`

### PlayStation 2

Install the [PCSX2]("https://github.com/PCSX2/pcsx2") manually.

Use custom arguments: `-batch -fullscreen -- {ImagePath}`

Inside the PCSX2 Settings, set a hotkey for "Exit Virtual Machine" to return to Playnite.

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
- I can`t find a way to exit using your controller, which makes it unusable for my controller-only setup.
