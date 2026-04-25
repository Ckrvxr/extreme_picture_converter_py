# Extreme Picture Converter

A collection of Python scripts for batch image conversion and compression, supporting **AVIF**, **JPEG XL**, and **PNG (Zopfli)** formats with multiple quality presets.

All scripts use **FFmpeg** under the hood and provide batch processing with progress tracking and file size comparison.

## Features

- **Batch conversion** — drop images into `input/`, run a script, get results in `output/`
- **Progress tracking** — real-time status per file with size comparison
- **Multiple quality presets** — from lossless to high compression
- **Auto-resize option** — scale images to max 2048px while maintaining aspect ratio (Lanczos resampling)
- **Wide input support** — JPG, PNG, BMP, TIFF, WebP, AVIF (and JXL for JXL script)
- **Three output formats** — AVIF (libaom-av1), JPEG XL (libjxl), PNG (zopflipng)

## Scripts Overview

All scripts are located in the `source/` directory. Run them from the project root.

### AVIF (libaom-av1)

| Script | CRF | Resize (2048px) | Output Suffix | Use Case |
|--------|:---:|:----------------:|---------------|----------|
| `source/1. AVIF_Lossless.py` | 0 | No | `_Lossless.avif` | Maximum quality, lossless preservation |
| `source/2. AVIF_High_Quality.py` | 16 | No | `_High_Quality_Lossless.avif` | Visually lossless, good for archival |
| `source/3. AVIF_High_Quality_Resize.py` | 16 | Yes | `_High_Quality_Resize.avif` | High quality with size reduction |
| `source/4. AVIF_Middle_Quality.py` | 32 | No | `_Middle_Quality.avif` | Balanced compression/quality |
| `source/5. AVIF_Middle_Quality_Resize.py` | 32 | Yes | `_Middle_Quality_Resize.avif` | Good for web sharing |
| `source/6. AVIF_Low_Quality.py` | 48 | No | `_Low_Quality.avif` | Maximum compression, suitable for thumbnails |

> **CRF guide**: 0 = lossless → 16 = near-lossless → 32 = medium → 48 = high compression with visible loss. All use `-cpu-used 0` for best compression efficiency.

### JPEG XL (libjxl)

| Script | Quality | Effort | Output Suffix | Use Case |
|--------|:-------:|:------:|---------------|----------|
| `source/7. JXL_Lossless.py` | Lossless (distance=0) | 9 | `_Lossless.jxl` | Modern lossless format, excellent compression |

> Requires FFmpeg compiled with `--enable-libjxl`.

### PNG (Zopfli)

| Script | Method | Output Suffix | Use Case |
|--------|--------|---------------|----------|
| `source/8. PNG_Lossless.py` | ZopfliPNG (`--lossy_transparent`) | `_Optimized.png` | Best PNG compression for web use |

> Non-PNG inputs are first converted to PNG via FFmpeg, then compressed with **zopflipng**. Requires `zopflipng` installed separately.

## Requirements

- **Python 3**
- **FFmpeg** — must be in your system PATH
- **zopflipng** — only needed for `PNG_Lossless.py` (Google's [zopfli](https://github.com/google/zopfli) tool)

### FFmpeg Installation

| Platform | Command |
|----------|---------|
| **macOS** | `brew install ffmpeg` |
| **Linux** | `sudo apt install ffmpeg` (Debian/Ubuntu) or use your distribution's package manager |
| **Windows** | `scoop install ffmpeg` or download from [ffmpeg.org](https://ffmpeg.org) |

> **Note**: For JXL support, you may need a custom FFmpeg build with `--enable-libjxl`. Check your package manager for `ffmpeg-jxl` or similar.

### zopflipng Installation

| Platform | Command |
|----------|---------|
| **macOS** | `brew install zopfli` |
| **Linux** | `sudo apt install zopfli` (Debian/Ubuntu) |
| **Windows** | `scoop install zopfli` or build from [source](https://github.com/google/zopfli) |

## Usage

1. Create an `input/` folder in the project root
2. Place your images in `input/`
3. Run any script from the project root:

```bash
# Example: high quality AVIF with resize
python "source/3. AVIF_High_Quality_Resize.py"

# Example: JPEG XL lossless
python "source/7. JXL_Lossless.py"

# Example: PNG Zopfli optimization
python "source/8. PNG_Lossless.py"
```

4. Converted files will appear in the `output/` folder

## Quality Guide

| You want... | Use... |
|-------------|--------|
| **Maximum quality / archival** | `AVIF_Lossless.py` (CRF 0) or `JXL_Lossless.py` |
| **Near-lossless, smaller files** | `AVIF_High_Quality.py` (CRF 16) |
| **Good for web sharing** | `AVIF_Middle_Quality.py` (CRF 32) — with resize variant for photos |
| **Smallest AVIF possible** | `AVIF_Low_Quality.py` (CRF 48) |
| **Lossless PNG for web** | `PNG_Lossless.py` — best PNG compression |
| **Social media / email** | Any `_Resize.py` variant — limits to 2048px max dimension |

## Input Formats

| Script | Supported Input Extensions |
|--------|---------------------------|
| AVIF scripts (1–6) | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.tif`, `.webp`, `.avif` |
| JXL_Lossless.py | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.tif`, `.webp`, `.avif`, `.jxl` |
| PNG_Lossless.py | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.tif`, `.webp`, `.avif`, `.jxl` |

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.