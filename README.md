# Agent Use Cases

This project uses `uv` to manage Python dependencies and a local virtual environment.

## Python Version

Use Python 3.12 for the most stable install. Some dependencies, such as `psycopg[binary]`, may not provide wheels for newer Python versions like 3.14.

```powershell
uv sync --locked --python 3.12
```

If a `.venv` was already created with the wrong Python version, remove only the virtual environment folder and recreate it:

```powershell
Remove-Item -Recurse -Force .venv
uv sync --locked --python 3.12
```

## Setup

Create a `.env` file in the project root and add the required API keys and URLs. Do not commit `.env` to Git.

Install dependencies:

```powershell
uv sync --locked --python 3.12
```

Use this interpreter in VS Code:

```text
.venv\Scripts\python.exe
```

## Poppler

PDF processing requires Poppler command-line tools such as `pdftoppm`, `pdftocairo`, and `pdfinfo`.

Check whether Poppler is available:

```powershell
where.exe pdftoppm
where.exe pdftocairo
where.exe pdfinfo
```

On Windows, install Poppler with a system package manager rather than `pip`:

```powershell
winget install oschwartz10612.Poppler
```

## Notebook Notes

For Jupyter notebooks, call async code with `await` instead of `asyncio.run(...)`:

```python
result = await main()
```

Avoid `nest_asyncio.apply()` unless it is strictly required, because it can interfere with async libraries used by `py-zerox`, LiteLLM, and OpenAI clients.

## Encoding Notes

Windows may default to `cp949`, which can fail on characters such as `U+2022` bullet symbols. Markdown output should be written with UTF-8:

```python
path.write_text(text, encoding="utf-8")
```

Generated markdown files under `output/` are ignored by Git.
