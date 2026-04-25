# AVIFConverter

A simple Python script that converts images to high-quality AVIF format using FFmpeg.

## Features

- Supports multiple input formats: JPG, PNG, BMP, TIFF, WebP, AVIF
- High-quality AVIF output (CRF 16, libaom-av1 encoder)
- Auto-resize with maximum 2048px dimension while maintaining aspect ratio
- Lanczos resampling for high-quality downscaling
- Batch conversion with progress tracking
- File size comparison output

## Requirements

- Python 3
- FFmpeg (must be installed and available in your system PATH)

## Usage

1. Create an `input` folder in the same directory as the script
2. Place your images in the `input` folder
3. Run the script:

```bash
python "2. AVIFConverter_High_Quality.py"
```

4. Converted AVIF files will appear in the `output` folder

## FFmpeg Installation

- **Windows:** `scoop install ffmpeg` or download from [ffmpeg.org](https://ffmpeg.org)
- **macOS:** `brew install ffmpeg`
- **Linux:** `sudo apt install ffmpeg` or use your distribution's package manager

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.
