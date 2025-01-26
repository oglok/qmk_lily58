# QMK Userspace

This is a personal fork of the QMK userspace repository with my own personal keymap for an spanish Mac layout for the Lily58 Pro split keyboard.

This requires to have QMK installed on the system. In MacOS, just run:

`brew install qmk/qmk/qmk`

If there is any issue with dependencies, rerun the same command and it should fix itself.

## Howto build locally

1. Run the normal `qmk setup` procedure if you haven't already done so -- see [QMK Docs](https://docs.qmk.fm/#/newbs) for details.
1. Clone your fork to your local machine
1. `cd` into this repository's clone directory
1. Set global userspace path: `qmk config user.overlay_dir="$(realpath .)"` -- you MUST be located in the cloned userspace location for this to work correctly
    * This will be automatically detected if you've `cd`ed into your userspace repository, but the above makes your userspace available regardless of your shell location.
1. Flash normally: `qmk flash -kb lily58/rev1 -km oglok_mac_es -e CONVERT_TO=promicro_rp2040`

NOTE: this keymap forces the right side of the keyboard to be the master, so the USB-C cable must be connected to the right micro-controller. The CONVERT_TO environment variable is required as I'm using a RP2040-based controller with a Pro Micro/Elite-C compatible pinout, and most of this project is based on the AVR micro from Atmel.

Flashing should show you an output like this:

```
Ψ Compiling keymap with gmake -r -R -f builddefs/build_keyboard.mk -s flash KEYBOARD=lily58/rev1 KEYMAP=oglok_mac_es KEYBOARD_FILESAFE=lily58_rev1 TARGET=lily58_rev1_oglok_mac_es VERBOSE=false COLOR=true SILENT=false QMK_BIN="qmk" CONVERT_TO=promicro_rp2040 QMK_USERSPACE=/Users/rnoriega/workspace/qmk_lily58 MAIN_KEYMAP_PATH_1=/Users/rnoriega/workspace/qmk_lily58/keyboards/lily58/rev1/keymaps/oglok_mac_es MAIN_KEYMAP_PATH_2=/Users/rnoriega/workspace/qmk_lily58/keyboards/lily58/rev1/keymaps/oglok_mac_es MAIN_KEYMAP_PATH_3=/Users/rnoriega/workspace/qmk_lily58/keyboards/lily58/rev1/keymaps/oglok_mac_es MAIN_KEYMAP_PATH_4=/Users/rnoriega/workspace/qmk_lily58/keyboards/lily58/rev1/keymaps/oglok_mac_es MAIN_KEYMAP_PATH_5=/Users/rnoriega/workspace/qmk_lily58/keyboards/lily58/rev1/keymaps/oglok_mac_es


⚠ lily58/rev1: SPLIT_KEYBOARD in rules.mk is overwriting split.enabled in info.json
arm-none-eabi-gcc (Homebrew ARM GCC 8.5.0_2) 8.5.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Size before:
   text    data     bss     dec     hex filename
      0   36200       0   36200    8d68 lily58_rev1_oglok_mac_es_promicro_rp2040.uf2

Copying lily58_rev1_oglok_mac_es_promicro_rp2040.uf2 to qmk_firmware folder                         [OK]
Copying lily58_rev1_oglok_mac_es_promicro_rp2040.uf2 to userspace folder                            [OK]

Size after:
   text    data     bss     dec     hex filename
      0   36200       0   36200    8d68 lily58_rev1_oglok_mac_es_promicro_rp2040.uf2

Flashing for bootloader: rp2040
Waiting for drive to deploy...
Flashing /Volumes/RPI-RP2 (RPI-RP2)
Wrote 72704 bytes to /Volumes/RPI-RP2/NEW.UF2
```

When flashing, the command will wait for the RP2040 to enter in flash mode. Press twice the reset button from the keyboard to get it in bootloader mode and get the firmware flashed.

Just to be safe, flash the compiled firmware in both sides. In my personal case, the left micro-controller has an issue with USB-C power, so we need to power the left side via the TRS cable, and connect the USB-C to the computer just to flash the firmware.
