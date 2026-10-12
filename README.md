# TrueML Docs

Documentation for [TrueML](https://github.com/iamprasadraju/trueml), built with Sphinx and the Read the Docs theme.

## Requirements

- Python 3.14+
- [uv](https://docs.astral.sh/uv/)

## Setup

Clone the repository and enter the project directory:

```bash
git clone https://github.com/iamprasadraju/trueml-docs.git
cd trueml-docs
```

Install dependencies:

```bash
uv sync
```

## Project Structure

```text
trueml-docs/
├── docs/
│   ├── source/
│   │   ├── conf.py
│   │   ├── index.rst
│   │   ├── _static/
│   │   └── _templates/
│   ├── build/
│   ├── Makefile
│   └── make.bat
├── pyproject.toml
├── uv.lock
└── README.md
```

- `docs/source/` — documentation source files and Sphinx configuration.
- `docs/build/` — generated HTML output.
- `docs/source/conf.py` — Sphinx settings, including the theme.
- `docs/source/index.rst` — documentation homepage.
- `pyproject.toml` — project metadata and dependencies.
- `uv.lock` — locked dependency versions for reproducible environments.

## Development

### Start the live preview

From the repository root:

```bash
uv run sphinx-autobuild docs/source docs/build
```

Open the local URL printed in the terminal, usually:

```text
http://127.0.0.1:8000/
```

The server watches source files and rebuilds the documentation when changes are detected. Stop it with `Ctrl+C`.

### Build the HTML documentation

```bash
uv run sphinx-build -b html docs/source docs/build
```

Open the generated homepage on macOS:

```bash
open docs/build/index.html
```

### Clean the generated output

```bash
uv run sphinx-build -M clean docs/source docs/build
```

Then rebuild using the HTML build command above.

## Configuration

The Read the Docs theme is configured in `docs/source/conf.py`:

```python
html_theme = "sphinx_rtd_theme"
```

The required packages are managed through `uv`:

```bash
uv add --dev sphinx sphinx-rtd-theme sphinx-autobuild
```

If the project is documentation-only, `pyproject.toml` should include:

```toml
[tool.uv]
package = false
```

This prevents `uv` from trying to install the documentation repository as a Python package. Ensure the value is spelled `false`.

## Writing Documentation

Sphinx uses reStructuredText (`.rst`) by default.

For example, edit `docs/source/index.rst`:

```rst
TrueML Documentation
====================

Welcome to the TrueML documentation.

.. toctree::
   :maxdepth: 2
   :caption: Contents

   getting-started
```

Create `docs/source/getting-started.rst` for the corresponding page:

```rst
Getting Started
===============

Learn how to install and use TrueML.
```

Add each new page to the `toctree` in `index.rst` so readers can navigate to it.

## Troubleshooting

### `Expected a Python module at: src/trueml_docs/__init__.py`

The project is being treated as an installable Python package. For a documentation-only project, set `package = false` under `[tool.uv]`.

### TOML error: `invalid boolean, expected false`

TOML booleans must be lowercase. Use:

```toml
[tool.uv]
package = false
```

Not `fasle`, `False`, or `"false"`.

### `config directory doesn't contain a conf.py file`

Make sure you are using the correct source directory.

From the repository root:

```bash
uv run sphinx-build -b html docs/source docs/build
```

From inside `docs/source`:

```bash
uv run sphinx-build -b html . ../build
```

### `Not Found` in the browser

1. Confirm the build succeeds.
2. Check that `docs/build/index.html` exists.
3. Start `sphinx-autobuild` with the correct source and output paths.
4. Open the exact URL printed by the server, usually `http://127.0.0.1:8000/`.

## Useful Commands

| Task | Command |
|---|---|
| Install dependencies | `uv sync` |
| Add documentation dependencies | `uv add --dev sphinx sphinx-rtd-theme sphinx-autobuild` |
| Start live preview | `uv run sphinx-autobuild docs/source docs/build` |
| Build HTML | `uv run sphinx-build -b html docs/source docs/build` |
| Clean build output | `uv run sphinx-build -M clean docs/source docs/build` |
| Open generated homepage | `open docs/build/index.html` |

## License

See the repository's license information.
