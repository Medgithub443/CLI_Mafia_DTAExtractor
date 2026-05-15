# Mafia DTA Extractor (CLI)

A command-line tool to extract `.dta` archives from **Mafia: The City of Lost Heaven**.

This is a stripped-down CLI tool based on [Richard01CZ/Mafia_DTAExtractor](https://github.com/Richard01CZ/Mafia_DTAExtractor), adapted for batch use in modding pipelines.

## Usage

```text
dta_cli.exe extract <file.dta> [-o <output-dir>] [-q]
dta_cli.exe list
```

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

No explicit license. Code adapted from the original unlicenced repository by Richard01CZ. All rights to the original logic belong to the author.

## Credits

- Original: [Richard01CZ](https://github.com/Richard01CZ)
- CLI adaptation for Mafia Mod Installer
