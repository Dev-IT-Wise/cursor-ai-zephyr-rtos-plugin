---
name: "Build Application"
description: "Build, flash, or work with firmware using project scripts from firmware/scripts. Uses build.sh, build_sample.sh, flash.sh instead of raw west commands."
---
# Build Application

## Overview
Use this command when building, flashing, or working with the firmware application. Always use the scripts from **firmware/scripts/** — do not invoke `west build` or flash tools directly. The scripts handle workspace paths, board aliases, and options consistently.

## Scripts location
- **Always use:** `firmware/scripts/` (or `@firmware/scripts/` when referring in chat)
- Do **not** run raw `west build`, `west flash`, or manual ninja commands for the main firmware workflow. Use the project scripts instead.

## Steps

1. **Choose the right script**
   - **Main application build:** `firmware/scripts/build.sh`
   - **Build a Zephyr sample:** `firmware/scripts/build_sample.sh`
   - **Flash only (after build):** `firmware/scripts/flash.sh`

2. **Build the main application**
   - Run from workspace root: `./firmware/scripts/build.sh` or `firmware/scripts/build.sh` with desired options.
   - Common options: `-b splitr` (board), `-c`/`--clean` (pristine), `-f` (flash after build), `-d` (debug), `--build-dir DIR`, `--source-dir DIR`.
   - For BLE FOTA, serial shell, RTT, NUS: use the script’s `--bt-fota`, `--serial-shell`, `--rtt-console`, `--rtt-tracing`, `--nus` flags instead of editing config manually when possible.

3. **Build a sample**
   - Use `firmware/scripts/build_sample.sh` with `-s`/`--sample` or positional sample path, e.g. `./firmware/scripts/build_sample.sh -b splitr -s path/to/sample`.

4. **Flash**
   - After building: `./firmware/scripts/flash.sh`, or use `build.sh -f` to build and flash.
   - Options: `-d`/`--build-dir`, `-a`/`--app-only`, `-e`/`--erase`, `-r`/`--recover` as needed.

5. **When suggesting or generating build/flash commands**
   - Prefer invocations of `firmware/scripts/build.sh`, `firmware/scripts/build_sample.sh`, and `firmware/scripts/flash.sh` with the appropriate flags.
   - Use script paths relative to the workspace root (e.g. `./firmware/scripts/build.sh`).

## Checklist
- [ ] Used a script from `firmware/scripts/` rather than raw west/ninja
- [ ] Script path is correct (e.g. `./firmware/scripts/build.sh`)
- [ ] Options match the task (board, clean, flash, debug, etc.)
