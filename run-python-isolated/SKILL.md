---
name: run-python-isolated
description: "Create and use a uv-managed Python environment per project on Linux. Use for pytest, python script execution, dependency installation, interpreter selection, and virtual-environment handling without relying on the system Python environment."
---

# Run Python Isolated

Use this skill when Python work must run inside a project-specific `uv` environment instead of the system Python environment or a manually activated standard `venv`.

## When to Use
- Run a Python script.
- Run `pytest` or another Python module.
- Install or update Python packages.
- Select the Python interpreter for a command.
- Create or repair a project Python environment on Linux.

## Procedure
1. Detect the project root before running Python commands.
2. Check whether the project already has a `uv` environment, typically at `.venv/`.
3. If the project environment is missing and Python work is required, create it with `uv venv` from the project root.
4. For subprocesses or terminal commands, prepend the project environment's `bin` directory to `PATH`.
5. Set `VIRTUAL_ENV` to the absolute path of the project environment.
6. Invoke Python with the project environment interpreter directly instead of relying on system `python` or `pip`.
7. Install dependencies into the project environment only.

## Command Patterns
- Create environment: `uv venv`
- Run a script: `.venv/bin/python3 script.py`
- Run a module: `.venv/bin/python3 -m pytest`
- Install a package: `.venv/bin/python3 -m pip install <package>`
- Show interpreter path: `.venv/bin/python3 -c "import sys; print(sys.executable)"`

## Rules
- Never rely on the host system's global `python` or `pip` commands.
- Always use a project-local `uv` environment on Linux.
- Create the environment with `uv venv` when Python work requires it and no project environment exists.
- Do not create a standard `venv` environment.
- Do not use `sudo` or `Administrator` privileges.
- Do not install or download packages outside the active project environment.

## Failure Handling
- If `uv` is unavailable, report that the required environment manager is missing.
- If the project environment cannot be created or is invalid, report the failure and stop before using the system Python environment.
- If a task requires system packages or elevated privileges, stop and explain that the skill only supports the existing isolated environment.
- If a request conflicts with these rules, refuse that step and explain the supported command pattern.



