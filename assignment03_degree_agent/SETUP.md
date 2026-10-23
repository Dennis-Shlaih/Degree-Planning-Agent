# Setup: running Assignment 3 locally

This assignment runs on your own computer, not in Google Colab. Setup takes about 15 minutes. The steps work on macOS, Windows, and Linux; where a command differs, both versions are shown.

The notebook's first code cell checks your setup. If it fails, its message names the step below that fixes it.

## 1. Install the tools

- **uv**, which installs Python and the packages for you. Follow the instructions at https://docs.astral.sh/uv/getting-started/installation/. On macOS and Linux:

  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

  On Windows (PowerShell):

  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

  Close the terminal and open a new one, then check with `uv --version`.

- **VS Code** (https://code.visualstudio.com/), with the **Python** and **Jupyter** extensions from Microsoft (Extensions view, search for each).

You do not need to install Python yourself: uv installs Python 3.12 for this project.

## 2. Unzip the assignment

Unzip the assignment into a folder **whose path has no spaces**, for example `~/courses/assignment03_degree_agent` (macOS, Linux) or `C:\courses\assignment03_degree_agent` (Windows). Paths with spaces, and folders synced by OneDrive or iCloud, cause hard-to-read errors.

Keep the files together: the notebook reads the data from the `data/` folder next to it.

## 3. Open a terminal in the folder

In VS Code, choose **File → Open Folder…** and open the assignment folder. Then open a terminal with **Terminal → New Terminal**; it starts in that folder. Check that you see the notebook, `data/`, and `pyproject.toml`:

```bash
ls        # Windows: dir
```

## 4. Create the environment

```bash
uv sync
```

This creates a `.venv` folder inside the assignment folder and installs the exact package versions listed in `uv.lock`, the same for every team. Do not install packages with `pip`; if a package seems missing, see Troubleshooting.

## 5. Add your API key

Copy the template to a file named `.env`:

```bash
cp .env.example .env        # Windows: copy .env.example .env
```

Open `.env` in VS Code and replace the placeholder with your OpenRouter key, with no quotes and no spaces:

```
OPENROUTER_API_KEY=sk-or-...
```

Never paste the key into a notebook cell, and never submit the `.env` file.

## 6. Select the project's kernel

Register the project's environment as a Jupyter kernel (one command; it is split over three lines here):

```bash
uv run python -m ipykernel install --user \
  --name assignment03-degree-agent \
  --display-name "Python (assignment03-degree-agent)"
```

On Windows PowerShell, type it on one line without the `\`.

Then open `Assignment03_Degree_Planning_Agent.ipynb` in VS Code, click **Select Kernel** (top right), choose **Jupyter Kernel…**, and pick **Python (assignment03-degree-agent)**. If it is not listed, see Troubleshooting.

*Alternative without VS Code:* run `uv run jupyter lab` in the terminal and open the notebook in the browser tab that appears; it uses the project's environment.

## 7. Run the setup check

Run the first code cell of the notebook. It should print:

```
Setup OK: packages, data files, and API key found.
```

You are ready to start.

## Troubleshooting

**`warning: VIRTUAL_ENV=... does not match the project environment path .venv and will be ignored`**
Another Python environment is active in your terminal, for example from an earlier tutorial. The warning is harmless, because uv uses this project's `.venv` anyway. To make it go away, run `deactivate`, or open a new terminal.

**The setup check says "This is not the project's Python" or "Missing package"**
The notebook is running on the wrong kernel. Redo step 6 and make sure the kernel name at the top right of the notebook is **Python (assignment03-degree-agent)**. If the message persists, run `uv sync` again, then restart the kernel.

**The kernel is not listed in VS Code**
Run the registration command in step 6 again, then reload VS Code (**Cmd/Ctrl+Shift+P**, then **Developer: Reload Window**) and look under **Select Kernel → Jupyter Kernel…** again.

**The setup check says "Data files not found"**
The notebook was opened from another location, or it was moved away from the `data/` folder. Open the assignment folder itself in VS Code (step 3) and open the notebook from there.

**The setup check says "OPENROUTER_API_KEY not found"**
Check that the file is named exactly `.env` (on Windows, not `.env.txt`), that it is in the assignment folder next to the notebook, and that the line has no quotes or spaces. Then restart the kernel and run the setup check again. On macOS, Finder hides files whose names start with a dot; open the folder in VS Code to see them.

**`uv: command not found`**
Open a new terminal after installing uv. If it is still not found, follow the "Adding uv to your PATH" note on the uv installation page.
