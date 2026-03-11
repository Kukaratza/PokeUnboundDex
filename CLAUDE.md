# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains a Pokemon Unbound PC Dex database stored as an Apple Numbers spreadsheet (`Pokemon Unbound PC Dex.numbers`). The file contains sprite images and data for 962+ Pokemon entries from the Pokemon Unbound ROM hack.

## Data Structure

### Numbers File Format
The `.numbers` file is a compressed archive (ZIP format) containing:
- **Data/**: 962 PNG sprite images of Pokemon
- **Index/**: 40 .iwa files (Apple's proprietary binary format for spreadsheet data)
- **Metadata/**: Document metadata including Properties.plist and BuildVersionHistory.plist
- **preview images**: preview.jpg, preview-web.jpg, preview-micro.jpg

### Pokemon Image Naming Convention
Images follow the pattern: `{number}-pokemon-unbound-{name}-{id}.png`

Examples:
- `001-pokemon-unbound-bulbasaur-446.png`
- `020-pokemon-unbound-alolan-rattata-263.png`
- `071-pokemon-unbound-hisuian-growlithe-828.png`
- `095-pokemon-unbound-galarian-ponyta-366.png`

The naming includes:
1. **Dex number** (001-976): Sequential Pokemon identifier
2. **Variant prefix** (optional): alolan, galarian, hisuian, mega, gmax, etc.
3. **Pokemon name**: lowercase with hyphens
4. **ID suffix**: 3-digit number (purpose unclear, may be internal game ID)

### Pokemon Coverage
- Covers generations 1-8 including regional variants (Alolan, Galarian, Hisuian)
- Includes legendary and mythical Pokemon (Zacian, Zamazenta, Eternatus, Calyrex, etc.)
- Total entries: 962+ sprites with various forms

## Working with the Data

### Extracting the Numbers File
To access the raw data:
```bash
# Extract the .numbers file (it's a ZIP archive)
unzip "Pokemon Unbound PC Dex.numbers" -d extracted/

# Navigate to extracted content
cd extracted/

# View Pokemon sprites
ls Data/

# Count total sprites
ls Data/ | wc -l
```

### Accessing Specific Pokemon
```bash
# Find a specific Pokemon by name
ls Data/ | grep -i "pikachu"

# Find all regional variants
ls Data/ | grep -E "(alolan|galarian|hisuian)"

# Find Pokemon by dex number
ls Data/ | grep "^025-"
```

### Image Processing
All sprites are PNG format and can be processed with standard image tools:
```bash
# View image dimensions
file Data/001-pokemon-unbound-bulbasaur-446.png

# Batch convert or process images
for img in Data/*.png; do
  # Your processing commands here
done
```

## Development Notes

### File Format Limitations
- The .iwa files in Index/ are Apple's proprietary binary format and cannot be easily read without Apple's libraries
- To edit the spreadsheet data, use Apple Numbers on macOS or iOS
- For programmatic access, extract and work with the PNG sprites directly

### Data Integrity
- The document was created with Numbers version 26.0.0
- Original document UUID: AC803F6C-256D-405A-96DC-36B6579D1A07
- Spreadsheet format version: 26.0.0

### Regional Variant Identification
Regional variants can be identified by the prefix in the filename:
- `alolan-`: Alola region variants (Gen 7)
- `galarian-`: Galar region variants (Gen 8)
- `hisuian-`: Hisui region variants (Legends: Arceus)

## Common Tasks

### Creating a Pokemon Database
To extract Pokemon data into a more accessible format:
```bash
# Generate a CSV/JSON listing of all Pokemon
ls Data/ | sed 's/-pokemon-unbound-/-,/' | sed 's/-[0-9]\{3\}\.png$//' > pokemon_list.csv
```

### Searching for Pokemon
```bash
# Case-insensitive search by name
ls Data/ | grep -i "{pokemon_name}"

# Search by type or generation (requires additional metadata not in filenames)
```

### Batch Operations
When working with all sprites:
```bash
# Copy all sprites to a new directory
cp Data/*.png /path/to/destination/

# Process only regional variants
cp Data/*alolan*.png /path/to/alolan/
cp Data/*galarian*.png /path/to/galarian/
cp Data/*hisuian*.png /path/to/hisuian/
```
