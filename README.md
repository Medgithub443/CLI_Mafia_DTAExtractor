```markdown
# Mafia DTA Extractor (CLI)

A command-line tool to extract `.dta` archives from **Mafia: The City of Lost Heaven**.

This is a stripped-down CLI fork of [Richard01CZ/Mafia_DTAExtractor](https://github.com/Richard01CZ/Mafia_DTAExtractor), adapted for batch use in modding pipelines.

## Usage


dta_cli.exe extract <file.dta> [-o <output-dir>] [-q]
dta_cli.exe list


### Examples

```bash
# Extract A0.dta to current directory
dta_cli.exe extract "C:\Mafia\A0.dta"

# Extract to a specific folder
dta_cli.exe extract "A1.dta" -o ".\extracted\missions"

# Silent extraction (no per-file output)
dta_cli.exe extract "AA.dta" -o ".\tables" -q

# List known DTA types
dta_cli.exe list
```

### Options

| Flag | Description |
|------|-------------|
| `extract <path>` | Extract a DTA file |
| `-o <dir>` | Output directory (created if missing) |
| `-q` | Quiet mode — suppress per-file logging |
| `list` | Show known DTA types |

### Exit Codes

- `0` — Success (number of files printed to stderr)
- `1` — Error (bad arguments, file not found, decrypt failure)

## Build

Requires MinGW or MSVC with C++11 support. Link against `-static` for standalone binaries.

## License

MIT-style — see original [upstream repository](https://github.com/Richard01CZ/Mafia_DTAExtractor) for details.

## Credits

- Original: [Richard01CZ](https://github.com/Richard01CZ)
- CLI adaptation for Mafia Mod Installer
```

---

## README.md (Release v1.0-beta)

```markdown
# Mafia DTA Extractor CLI v1.0-beta

First beta release of the command-line DTA extraction tool.

## Quick Start

Download `dta_cli.exe` and run:

```
dta_cli.exe extract "A0.dta" -o ".\output"
```

## What's New

- Stripped to pure CLI — no GUI dependencies
- Batch-friendly exit codes for scripting
- Quiet mode for CI / installer pipelines
- All 16 known Mafia DTA types supported

## Usage

```
dta_cli.exe extract <input.dta> [-o <dir>] [-q]
dta_cli.exe list
```

## Known DTA Types

| File | Description |
|------|-------------|
| A0.dta | Sounds |
| A1.dta | Missions |
| A2.dta | Models |
| A3.dta | Animations I |
| A4.dta | Animations II |
| A5.dta | Diff Data |
| A6.dta | Textures |
| A7.dta | Records |
| A8.dta | Patch Files |
| A9.dta | System |
| AA.dta | Tables |
| AB.dta | Music |
| AC.dta | Animations III |

## Notes

- Beta status — report issues on GitHub
- Requires Windows XP or later
```
