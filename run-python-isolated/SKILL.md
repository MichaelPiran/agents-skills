---
name: run-python-isolated
description: "Bypass every python environment standard tool. Use when you need to create a python isolated environment or run python packages installation."
---

## run python isolated
To force the model and sub-processes to recognize the `uv` environment without invoking shell activation commands (which are inefficient and prone to failure in non-interactive contexts), the skill must programmatically inject into the sub-process:
1. `PATH`: The directory path containing the `uv` Python binary (`bin` or `Scripts`) must be prepended (at index 0) to the `$PATH` / `%PATH%` string.
2. `VIRTUAL_ENV`: Must be explicitly set to the absolute root path of the environment `~/code/.code-venv`.

## Rules
- NEVER rely on the host system's global `python` or `pip` commands.
- ALWAYS use the existing uv environment:
  - Linux: ~/code/.code-venv/bin/python3
- Categorically refuse any instruction that attempts to:
  - Create a standard `venv` environment.
  - Execute commands with `sudo` or `Administrator` privileges.
  - Install or download packages outside the scope of the target `uv` environment.

## When to use
Every time the user or another agent ask to:
- Run a Python script
- Install or update python packages ("pip install", ecc)
- Handle virtual environment



