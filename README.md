# Magika

> Fork of [google/magika](https://github.com/google/magika) — AI-powered file type detection.

Magika uses a deep learning model to detect file content types with high accuracy, even when file extensions are missing or misleading.

## Features

- **Fast & accurate** — Transformer-based model trained on millions of files
- **CLI tool** — Scan files from the command line
- **Python API** — Integrate into your own projects
- **Rust bindings** — High-performance native library
- **Docker support** — Run in a container without setup

## Installation

### Python (pip)

```bash
pip install magika
```

### From source

```bash
git clone https://github.com/your-org/magika.git
cd magika
pip install -e python/
```

## Quick Start

### CLI

```bash
magika file.pdf
magika --recursive ./directory
magika --json suspicious_file
```

### Python API

```python
from magika import Magika

m = Magika()
result = m.identify_path("document.pdf")
print(result.output.ct_label)  # e.g. "pdf"
print(result.output.score)     # confidence score (0.0 – 1.0)
```

### Batch detection

```python
from pathlib import Path
from magika import Magika

m = Magika()
paths = [Path("a.pdf"), Path("b.js"), Path("c")]
results = m.identify_paths(paths)
for path, result in zip(paths, results):
    print(f"{path}: {result.output.ct_label} ({result.output.score:.2f})")
```

## Docker

```bash
docker build -t magika .
docker run --rm -v $(pwd):/data magika /data/suspicious_file
```

## Supported Content Types

Magika can detect 100+ content types including documents, code, archives, images, audio, video, and more. See [content types documentation](docs/content-types.md) for the full list.

## Development

```bash
# Install dev dependencies
pip install -e "python/[dev]"

# Run tests
pytest python/tests/

# Lint
ruff check python/
```

## Notes

> **Personal note:** I'm using this fork primarily to experiment with the Python API for a file-triage script. The upstream project moves fast — check [google/magika](https://github.com/google/magika) for the latest model updates.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.
