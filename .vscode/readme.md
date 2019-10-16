# VSCode and STM32 development

I used this guide as a starting point: ["Using Visual Studio Code with STM32CubeMX for ARM Development"](https://hbfsrobotics.com/blog/configuring-vs-code-arm-development-stm32cubemx)

Some great stuff in that article! However I did make some notable changes in order to build for the BWhoop B03 hardware. In particular
I'm using OpenOCD for both flashing the firmware as well as for debugging it.

The original article describes creating a `C:\VSARM` folder to contain the set of tools needed for this VSCode workflow.
However I already have a `C:\Tools` folder that I use for tools like this so that is where we'll install them.

## Install arm gnu toolchain

Go to: <https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads>
Download the Windows installer. There are several available. I chose:

```
gcc-arm-none-eabi-8-2019-q3-update-win32-sha2.exe
Windows 32-bit Installer (Signed for Windows 7 and later)
MD5: d44f44b258b203bdd6808752907754be
```

Run the installer. When it prompts you to "Choose Install Location" I changed the default shown in "Destination Folder"
from:

```
C:\Program Files (x86)\GNU Tools ARM Embedded\8 2019-q3-update
```
to 
```
C:\Tools\armcc
```

## Install MinGW-W64

Go to: <https://sourceforge.net/projects/mingw-w64/>
Change the install location to `C:\Tools\mingw`

We use this for `make`.

## Install st-link tools
> Note: You can disregard this. I gave up on using this tool but am keeping these notes in case I decide to revisit
Go to: <https://github.com/texane/stlink/releases>
Get the binaries and install into: `C:\Tools\stlink`
Unfortunately there hasn't been a recent release of binaries and the most recent one
is version 1.3.0 from Jan 28, 2017: [stlink-1.3.0-win64.zip](https://github.com/texane/stlink/releases/download/1.3.0/stlink-1.3.0-win64.zip)


## Install OpenOCD
Go to: <https://gnutoolchains.com/arm-eabi/openocd/>

Download the most recent 7zip file: `openocd-20190828.7z`
Decompress it into `C:\Tools` folder. Rename the resultant `OpenOCD-20190828-0.10.0` folder to just `OpenOCD`.

### ST-Link V2
I'm using a clone ST-Link V2 probe purchased from Amazon: <https://www.amazon.com/gp/product/B01EE4WAC8/>. I had installed the "ST-Link Utility"
from here: <https://www.st.com/en/development-tools/stsw-link004.html>

I'm pretty sure that's how I ended up getting the st-link drivers installed onto my Windows 10 development machine. I also ended up updating
the firmware on my ST-Link V2 probe using that utility but I'm not sure if that was necessary. I'm noting it here in case it may be useful.

## VSCode
Hit F1 key and enter "select default" and choose the "Terminal: Select Default Shell". Then choose "Command Prompt C:\WINDOWS\System32\cmd.exe".

Choose "Git Bash C:\Program Files\Git\bin\bash.exe". This will let us access all of the Windows executables we installed, but also allow
us to use `bash` commands like `rm`. This is especially helpful because the `clean` target in the `Makefile` uses the `rm -f` command.

