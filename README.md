# BlackHatLab Bundle Ripper

A dnSpyEx Extension that opens .NET Single-File Bundles (v1/v2/v6) inside dnSpyEx  
Grouped Bundle Explorer with search, sort and open, single/multi/Extract-All export  
And one-click **RePack Bundle** beside **Save All**.

![Version](https://img.shields.io/badge/version-3.1.0-blue)
![Runtime](https://img.shields.io/badge/dnSpyEx-net48_%7C_net10-purple)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)

Developed by **Dr.FarFar** — Member of the eXeTools Family
Crafted For the .NET community.

---

## Features

| Area | What you get |
|---|---|
| **Bundle detect** | Auto-detect on File > Open, drag & drop, `Open With`, and command-line files — silent skip for non-bundles, no popups |
| **Bundle Explorer** | Dockable view (`Debug > Windows`, bottom next to Locals), multi-bundle grouped rows, collapse/expand, live search (250 ms debounce), click-to-sort columns |
| **Open** | Double-click / `Open` extracts the file to the work folder and opens it in dnSpy — heavily obfuscated payloads never auto-open |
| **Extract** | Single file (`Save As`), multi-selected files (modern folder picker), **Extract All** into per-bundle subfolders with progress status |
| **Folder picker** | Native Vista `IFileOpenDialog` + `FOS_PICKFOLDERS` — identical modern dialog on net48 and net10, `Select Folder` button, WinForms fallback |
| **Work folder** | System Temp by default or custom folder, cache limit (GB), **Clear Cache Now**, free-space readout, extract mode (`All Upfront` / `Assemblies Only` / `On Demand`), max single-file cap (MB) |
| **Cache** | Oldest-first eviction so any number of opened bundles can never fill the drive — runs off the UI thread, never evicts the just-opened bundle |
| **RePack** | `File > RePack Bundle` (same SaveAll icon): same-size edits inject in place, grown assemblies prompt a full rebuild (offsets + manifest + apphost placeholder) with `.bak` backup and rebuilt-image verification |
| **Parser** | Streaming v1/v2/v6 parse (10 MB tail only, never loads the whole exe — x86 and 2 GB+ safe), v6 Deflate decompression, DepsJson/RuntimeConfig/Flags handling |
| **Safety** | Path-traversal guards on every write, temp-copy commit (live exe never torn on crash), chunked extract/compare with constant memory |
| **Options page** | `Tools > Options > BlackHatLab > Bundle Ripper` plus shared BlackHatLab welcome node listing all installed BlackHatLab extensions A–Z |

---

## Screenshots

![About](screenshots/01-%20About.png)
*About dialog*

![Options 1](screenshots/02-%20Options%201.png)
*Options page — Work Folder, Cache*

![Options 2](screenshots/03-%20Options%202.png)
*Options page — Extraction mode*

![Debug Windows](screenshots/04-%20Debug%20-%20Windows.png)
*Opening the explorer via Debug > Windows*

![Bundle Explorer](screenshots/05-%20Bundle%20Explorer%201.png)
*Bundle Explorer — grouped multi-bundle view*

![Right Click Menu](screenshots/06-%20Bundle%20Explorer%20-%20Right%20Click%20Menu.png)
*Right-click menu — Open / Extract This File*

![Open Multi Files 1](screenshots/07-%20Open%20Multi%20Files%201.png)
*Opening multiple files 1*

![Open Multi Files 2](screenshots/08-%20Open%20Multi%20Files%202.png)
*Opening multiple files 2*

![Assembly Explorer After Open](screenshots/09-%20Assembly%20Explorer%20After%20Open.png)
*Assembly Explorer after open*

![Extract Multi Files](screenshots/10-%20Extract%20Multi%20Files.png)
*Extracting multiple files*

![Extract Multi Files 2](screenshots/11-%20Extract%20Multi%20Files%202.png)
*Extracting multiple files 2*

![RePack Bundle](screenshots/12-%20RePack%20Bundle.png)
*RePack Bundle entry beside Save All*

![Repacked](screenshots/13-%20Repacked.png)
*Repacked confirmation*

---

## Installation

1. Download the Release archive from the [Releases](https://github.com/BlackHatLab-INC/BlackHatLab-Bundle-Ripper/releases) page:
   - `BlackHatLab Bundle Ripper - .NET Framework 4.8.zip` for classic dnSpy / dnSpyEx net48
   - `BlackHatLab Bundle Ripper - .NET 10.zip` for dnSpyEx .NET 10 builds
2. Extract the release archive into your dnSpyEx `Extensions` folder:
   - `bin\Extensions\BlackHatLab Bundle Ripper\`
3. Restart dnSpyEx.
4. Open any Single-File `.exe` — the Bundle Explorer appears automatically (`Debug > Windows > Bundle Explorer` to reopen it).

> Requires - dnSpyEx on Windows (AnyCPU — works on x86 and x64). No extra dependencies.

---

## Usage

- **Open a bundle:** `File > Open` any Single-File `.exe` — embedded files list in the explorer grouped per bundle.
- **Search / sort:** type in `Search`, click column headers to sort, double-click a bundle header to collapse/expand it.
- **Open files:** double-click or right-click `Open` — the file is extracted to the work folder and opened in dnSpy.
- **Extract:** right-click `Extract This File...` for one file, select many + `Extract` for bulk, or **Extract All...** to dump every bundle into per-bundle subfolders.
- **Edit + RePack:** edit IL in dnSpy → `Save All` (saves the dll) → **`File > RePack Bundle`** (same SaveAll icon, right beside it):
  - Same-size edits inject in place, manifest untouched, timestamped `.bak` kept next to the exe.
  - Grown assemblies ask for a full rebuild — offsets shift, manifest is rewritten, the apphost placeholder is patched, and the rebuilt image is re-parsed to verify before commit.
- **Options:** `Tools > Options > BlackHatLab > Bundle Ripper` — work folder, cache limit, extract mode, per-file cap. `Tools > Options > BlackHatLab` shows the welcome page with every installed BlackHatLab extension.

---

## Notes

- Non-bundle files are silently skipped on auto-scan (logged only) — a normal assembly never pops an error.
- Every output path is containment-checked (no path traversal, no escape from the chosen folder).
- Large bundles stream chunk-by-chunk (1 MB) — constant memory on x86 and safe for 2 GB+ exes.
- RePack commits via temp-copy + `File.Replace` — the live exe is never left half-written on crash.

## License

Copyright © 2026 Dr.FarFar. All Rights Reserved.

This software is provided for personal use only. Redistribution, modification, or republishing without prior written permission from Dr.FarFar is prohibited.

## Credits

- Dr.FarFar (eXeTools Family)
