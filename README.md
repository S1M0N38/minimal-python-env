# Minimal Python Environment

<p align="center">
  <img src="https://raw.githubusercontent.com/S1M0N38/minimal-python-env/main/snake.svg" alt="Snake Logo" width="200"/>
</p>

Managing Python environments can be made simple with the built-in [`venv`](https://docs.python.org/3/library/venv.html) library. While many people use [`virtualenv`](https://virtualenv.pypa.io/en/latest/index.html) or [`conda`](https://docs.conda.io/projects/conda/en/latest/commands/index.html) for this purpose, the built-in `venv` library is more than sufficient for most use cases.

## Setup Instructions

Copy the following lines into your `bashrc` or `zshrc` file to streamline the process of creating and managing Python virtual environments:

```bash
## Minimal Python Environment 
## https://github.com/S1M0N38/minimal-python-env

# Function to create a virtual environment and optionally install dependencies
pye() {
    python -m venv --upgrade-deps .venv

    echo -n "Do you want to install dependencies from requirements.txt? (yes/no) [yes]: "
    read choice
    choice=${choice:-yes}

    case "$choice" in 
        yes|Yes|y|Y ) .venv/bin/python -m pip install -r requirements.txt;;
        * ) echo "Skipping requirements installation.";;
    esac
}

# Function to activate the virtual environment
pya() {
    if [ -d ".venv" ]; then
        source .venv/bin/activate
    else
        echo "Virtual environment not found. Please create it first using 'pye'."
    fi
}

# Function to run Python scripts within the virtual environment without activating it
py() {
    if [ -f ".venv/bin/python" ]; then
        .venv/bin/python "$@"
    else
        echo "Virtual environment not found. Please create it first using 'pye'."
    fi
}
```

After adding the above lines to your `bashrc` or `zshrc` file, source it.

## Usage

- **Create a virtual environment:**

  Run the following command to create a virtual environment and optionally install dependencies from `requirements.txt`:

  ```bash
  pye
  ```

- **Activate the virtual environment:**

  To activate the virtual environment, use:

  ```bash
  pya
  ```

- **Run Python scripts within the virtual environment without activating it:**

  You can directly run Python scripts using the virtual environment's Python interpreter without activating the environment:

  ```bash
  py your_script.py
  ```
