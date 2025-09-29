# Package Management with `uv`

To ensure that everyone can easily run your project code without worrying about matching package versions, you can use `uv` as the package management tool. It's similar to `pip` but significantly faster, has a syntax reminiscent of `poetry`, and offers several additional useful features.

## Installing `uv` (Linux)

To install `uv`, run the following commands:
- `sudo apt update` 
- `pip install uv` 

This might raise the error ***externally managed environment***.

### Alternative installation (recommended)
If `curl` is not installed yet, add the program via 
- `sudo apt-get install curl`.

Then run:
- `curl -LsSf https://astral.sh/uv/install.sh | sh`,

**Do not run** this with sudo, or the package will be installed in the root directory. 

After installation, follow the terminal instructions and run:
- `source $HOME/.local/bin/env` to add it to PATH

Verify the installation with:
- `uv --version`

If you run into a 'command not found' issue, add `uv` to your path manually:

- `export PATH="$HOME/.local/bin:$PATH"` (adding it to your `.bashrc` or `.zshrc` file
  makes it permanent)

## Project Setup
Now, to initialize a new project and create a virtual environment, run:

- `uv init`
- `uv venv`

The commands initialize your project and create a `.venv` folder that stores your virtual environment.

### Installing Dependencies

If you’ve cloned a repository that already uses uv (and contains a pyproject.toml file), install all dependencies with:
- `uv sync --all-groups`

This syncs the environment with the packages listed in the pyproject.toml.

### Activating & Deactivating the Virtual Environment
To activate or deactivate a virtual environment, run:

- `source .venv/bin/activate`
- `deactivate`

### Adding & Removing Packages
To add and remove packages to the virtual environment, run:

- `uv add <package_name>`
- `uv remove <package_name>`
