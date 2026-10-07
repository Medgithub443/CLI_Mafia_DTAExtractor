# Mafia DTA Extractor (CLI)

A command-line tool to extract `.dta` archives from **Mafia: The City of Lost Heaven**.

This is a stripped-down CLI tool based on [Richard01CZ/Mafia_DTAExtractor](https://github.com/Richard01CZ/Mafia_DTAExtractor), adapted for batch use in modding pipelines.

Current version: **1.1.0 Beta** (`dta_cli.exe version`).

## Usage

```text
dta_cli.exe extract <file.dta> [-o <output-dir>] [-q]
dta_cli.exe extract-safe <file.dta> [-o <output-dir>] [-q]
dta_cli.exe extract-all <dir-with-dtas> [-o <output-dir>] [-q]
dta_cli.exe list
dta_cli.exe version
```

### Examples

```bash
# Extract A0.dta to current directory
dta_cli.exe extract "C:\Mafia\A0.dta"

# Recommended for single archives: also auto-applies the A8.dta patches
dta_cli.exe extract-safe "C:\Mafia\AA.dta" -o "C:\Mafia"

# Extract to a specific folder
dta_cli.exe extract "A1.dta" -o ".\extracted\missions"

# Silent extraction (no per-file output)
dta_cli.exe extract "AA.dta" -o ".\tables" -q

# Extract EVERY .dta from the game folder into the game folder itself,
# with the patch archive A8.dta automatically applied last
dta_cli.exe extract-all "C:\Mafia"

# Same, but into a separate output directory
dta_cli.exe extract-all "C:\Mafia" -o "D:\Mafia unpacked" -q

# List known DTA types
dta_cli.exe list
```

### Options

| Flag | Description |
|------|-------------|
| `extract <path>` | Extract a single DTA file |
| `extract-safe <path>` | Same, then auto-extracts `A8.dta` (patches) from the same folder right after |
| `extract-all <dir>` | Extract every `.dta` found in `<dir>` |
| `-o <dir>` | Output directory (created if missing). Default: current dir for `extract`/`extract-safe`, the scanned dir itself for `extract-all` |
| `-q` | Quiet mode — suppress per-file logging |
| `list` | Show known DTA types |
| `version` | Print version (`--version`, `-v` also work) |

### Exit Codes

- `0` — Success
- `1` — Error (bad arguments, file not found, decrypt failure, or at least one archive failed in `extract-all`)

## Important: A8.dta is a patch archive — order matters

`A8.dta` ("Patch Files") contains **patched copies of files that also exist in other
archives**: `tables/carcyclopedia.def`, `tables/carindex.def`, `tables/load.def` (also
in `AA.dta`), `tables/MENU/*.mnu` (only in A8), `SYSTEM/ddsegment*.sav` (only in A8),
plus updated `MISSIONS/*/tree.klz`, `MODELS/*.4ds`, `MAPS/*.bmp` (also in `A1.dta`,
`A2.dta`, `A6.dta`).

Mafia prefers loose files over archive content, so **whatever is extracted last wins**.
If `A8.dta` is unpacked *before* the archives it patches, the original (unpatched) files
overwrite the patches, which manifests as garbage menu strings (e.g. car names in
free-ride showing raw internal ids like `fordtto` instead of "Bolt Ace Tudor") or
crashes. This is exactly what the upstream GUI tool prevents by moving A8.dta to the
end of the extraction queue.

`extract-all` and `extract-safe` enforce this rule automatically: `extract-all`
orders the archives (alphabetical, `A8.dta` last), and `extract-safe` applies
`A8.dta` right after the requested file. If you script the plain single-file
`extract` command yourself, you must apply the same ordering: `A8.dta` always
goes **last**.

## Changelog

### 1.1.0 Beta
- Added `extract-all <dir>`: unpacks every `.dta` in a folder in one run, with
  `A8.dta` (patch archive) always extracted last — mirrors the upstream GUI tool
  behaviour and fixes broken menus / car names caused by wrong extraction order.
- Added `extract-safe <file.dta>`: like `extract`, but automatically applies the
  `A8.dta` patch archive (taken from the same folder) right after the requested
  archive — the recommended mode for one-off single-archive unpacking.
- Added `version` / `--version` / `-v`.
- Hardened `extract` against corrupt file headers (no more huge `reserve()` on
  garbage `FileSize`).
- `extract -o` path is now resolved to absolute before changing directory.

### 1.0
- Initial CLI port of Richard01CZ/Mafia_DTAExtractor.

## Build

MinGW-w64 / w64devkit (GCC) with `-static` for a standalone binary:

```bash
g++ -O2 -std=c++11 -static -o dta_cli.exe dta_cli.cpp
```

MSVC (`cl /O2 /EHsc dta_cli.cpp`) works as well.

## License

No explicit license. Code adapted from the original unlicenced repository by Richard01CZ. All rights to the original logic belong to the author.

## Credits

- Original: [Richard01CZ](https://github.com/Richard01CZ)
- CLI adaptation for Mafia Mod Installer
