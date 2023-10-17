# C64PECTRE

Research & development on Commodore and related technologies
https://github.com/c64pectre.

# Setting up the CMD-HD Hard Drive with a C64 in VICE Emulator

https://github.com/c64pectre/c64-cmd-hd

## Preparation

- Buy a "CMD HDD Boot ROM 2.80 Binary Image" at Retro Innovations
    https://store.go4retro.com/commodore/cmd-hdd-boot-rom-2-80-binary-image/.
    It is still licenced software, not abandonware.

- Find and download the "CMD Hard Drive Utilities", e.g. from
    https://commodore.software/downloads/download/94-cmd-hard-drive/8016-cmd-hard-drive-utilities/

- Find and download the "CMD Hard Drive Users Manual for all CMD HD Models 4th edition jan 1991",
    e.g. from https://archive.org/details/CMD_Hard_Drive_Users_Manual_4th_Edition_Jan_1991
    This document describes all commands that you'll need to know about when
    using the hard drive.

## Steps

1. Create an empty DHD file:

        copy nul cmd-hd-a.dhd

1. Configure VICE

    1. In Preferences > Settings (`ALT+O`) > Machine > ROM > Drive ROMS:
        change the CMD HD entry to your real CMD HDD Boot ROM 2.80 Binary Image.
        You can copy the file to the `DRIVES` folder in your VICE folder.

    1. In Peripheral devices > Drive > Drive 9: at Drive model, choose
        "CMD HD", set a CMD-HD size of at least `20M` (suggestion: `512M`),
        check the checkbox "Save real-time clock data".

    1. Attach disk image for drive `9` to your DHD file.

    1. Do a hard reset of the C64.

1. Create HD System

    1. Attach disk image for drive `8` to `cmd-hd-tools.d64`.

    1. Load and run `CREATE SYS` from `8`. Press `RETURN` in the welcome screen.
        Accept default with `RETURN`.
        Press `Y` to clear area below system.

    1. When finished, do a hard reset of the C64.

1. Create Partition

    1. Load and run `HD-TOOLS.64` from `8`.

    1. Ignore welcome screen instructions (not needed).

    1. Reset Drive `9` to its configuration mode: click on drive `9` in the
        status bar and click on "Configuration Mode".

    1. View current partition table. Should all be not in use. `RETURN` to exit.

    1. Create a new partition:

            001 ROOT 65280 NATV

        The `NATV` means native partition. Press `-` in BLKS to get the max.
        Create more partitions if you want.

    1. Do a hard reset of the C64.

## Explore the HD

Consult the "CMD Hard Drive Users Manual for all CMD HD Models 4th edition jan
1991" to learn about all possible commands.

Change to device `9`:

    @9

List current (root) directory:

    @$

### Copy "CMD Hard Drive Utilities" to the HD

1. First, create a subdirectory for the HD Utilities on the HD:

        @MD:CMD-HD-TOOLS

1. Load and run `FCOPY` from `8`.

1. Copy `8` to `9` to subdirectory `//CMD-HD-TOOLS/`.
