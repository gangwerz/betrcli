# **The** BETR command-line interface

A command-line abstraction for [btrfs](https://btrfs.wiki.kernel.org/index.php/Main_Page).

## Goals

This project is aiming to bring a cli-based mounting system. The primary goal is to replicate the conveniences of the ZFS cli for btrfs, and maybe arbitrary filesystems.

The primary inspiration is the subvolume management in btrfs. Coming from ZFS, being unable to define properties, flags, and mount points from commands was very inconvenient. Going back to editing `/fstab` felt like a step backwards

### 1.0.0 Goals

- CLI to define non-root subvolumes mountpoints and mount parameters
    - Save configs as YAML files to allow for easy manual editing
- Automount subvolumes at boot time
    - Systemd service
    - Configs should be saved to `/etc` to allow for a `/var` subvolume
        - Systemd service will need to contain the mount commands directly, without calling `betr`? Service file would then need updated after every change
        - Store executable in `/sbin` to be included outside of `/usr`?

### Proposed Features

These are all features that would be great to have, but need to be reviewed, researched, and roadmapped.

- Subvolume creation
- RAID creation
- Add and configure caching
- Information and data
    - Print all data available from [`btrfs`](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs)
    - Provide wrapper to [`compsize`](https://github.com/kilobyte/compsize)
    - Standardize output formatting

## Potential Shortcomings & Proposed Solutions

- Cannot directly handle mounting `/` as the config files need to be read from somewhere
    - To assist in root mounting, provide `betr print fstab <subvolume>` to print a suggested FSTAB entry.