# Setting up a Working Environment with WSL

When primarily working on Windows but wanting to develop in a Linux environment, the **Windows Subsystem for Linux (WSL)** provides a convenient solution. In this guide, we use the **Debian** distribution instead of the default **Ubuntu**, so all development will take place in a **Debian shell**. The recommended editor is **VS Code**, though **PyCharm (Community Edition)** or any other Python IDE should work as well.


### 1. Install Windows Subsystem for Linux (WSL)

To install WSL, open a Windows terminal and run:

- `wsl --install` in a Windows terminal
- restart your machine, if prompted

### 2. Set Up Debian Shell with Python and Git

By default, WSL installs Ubuntu. If Debian is not installed, you can download it from the **Microsoft Store**.

Once Debian is installed, launch it from your Start menu, then run the following commands:

- `sudo apt update && sudo apt upgrade -y` (for updating packages)
- `sudo apt install python3 python3-pip git -y` (install Python and Git)

### 3. Install VS Code (or another code editor)

- Download it from https://code.visualstudio.com
- Install the `WSL` extension in VS Code (Extensions -> Search "WSL" ->
  Install)

### 4. Access the Debian Shell from Within VS Code

- Press `Ctrl+Shift+P` -> type `WSL: Connect to WSL in New Window` (should open a VS Code
  window connected to your Debian shell; you should now be able to run Debian shell
  commands inside VS Code's terminal).