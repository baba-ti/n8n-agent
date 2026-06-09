# Agent Use Cases

This project uses `uv` to manage Python dependencies and a local virtual environment.

## Python Version

Use Python 3.12 for the most stable install. Some dependencies, such as `psycopg[binary]`, may not provide wheels for newer Python versions like 3.14.

```powershell
uv sync --locked --python 3.12
```

If a `.venv` was already created with the wrong Python version, remove only the virtual environment folder and recreate it:

## Setup

Create a `.env` file in the project root and add the required API keys and URLs. Do not commit `.env` to Git.

Install dependencies:

```powershell
uv sync --locked --python 3.12
```

## Encoding Notes

Windows may default to `cp949`, which can fail on characters such as `U+2022` bullet symbols. Markdown output should be written with UTF-8:

```python
path.write_text(text, encoding="utf-8")
```

Generated markdown files under `output/` are ignored by Git.
