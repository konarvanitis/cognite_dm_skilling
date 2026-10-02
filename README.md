# cognite_dm_skilling
This repository provides the base code for Academy learners to follow the Data Modeling course

## Getting Started

### Prerequisites

- Python 3.11, 3.12 or 3.13
- [uv](https://docs.astral.sh/uv/)

### 1. Install dependencies

```bash
uv sync
```

This installs the dependencies defined in `pyproject.toml` (pinned in `uv.lock`) and creates a virtual environment (`.venv`) in the project folder.

### 2. Configure credentials

Copy `.env.template` to `.env` and fill in your CDF details.

### 3. Run the notebooks / Toolkit

Open the repo in your IDE (e.g., VS Code) and select the `.venv` interpreter as your kernel. CLI tools run through uv, e.g. `uv run cdf --help`.

## Additional notes for developers

### Add new libraries as needed

```bash
uv add pandas numpy
```

or if only required for development

```bash
uv add --dev pytest
```

### Set up clean notebook diffs (one-time, per clone)

Jupyter stamps your local kernel name and Python version into each notebook's metadata every time you run it, which shows up as noisy, unrelated diffs in `git status`/`git diff`. Run this once after cloning to strip that noise before it ever reaches git:

```bash
uv run nbstripout --install --attributes .gitattributes
git config filter.nbstripout.extrakeys "metadata.kernelspec metadata.language_info.version metadata.vscode"
```

This registers a git filter that strips outputs, execution counts, and the kernel/version/VS Code interpreter metadata from notebooks whenever git reads or diffs them — your local `.ipynb` files on disk are untouched, so notebooks still run and show outputs normally in your editor.

The filter lives in your local `.git/config`, so it is not shared through the repo. To catch anyone who skipped this step, CI fails a PR if a committed notebook still contains outputs or kernel metadata. If that happens, run the two commands above, then `git add --renormalize .` and commit.

Copyright 2025 Cognite AS
