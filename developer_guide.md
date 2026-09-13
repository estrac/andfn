## How to Install VS Code IDE for the `andfn` Package on Ubuntu

### Install Python on the system
    `sudo apt update`
    `sudo apt install python3 python3-pip python3-venv -y`

### Install and Configure Git on the system
Follow the instructions for installing and configuring `git` that are stored in the Mlaem repository on GitHub. These instructions are located at [https://github.com/ODLS1/Mlaem/tree/main/readme/Git_Config.md](https://github.com/ODLS1/Mlaem/tree/main/readme/Git_Config.md).

### Fork the `andfn` repository on GitHub
* Fork the `andfn` repository on GitHub using the GitHub Website GUI.
    - Search for "andfn"
    - Click on the `andfn` repository
    - Click on `Fork`
    - Follow GitHub instructions

### Install VS Code (citation: Google AI)
The best and most reliable way to install Visual Studio Code on Ubuntu is by downloading and installing the official `.deb` package from Microsoft. This native installation method ensures that the official package repository is configured automatically, allowing you to receive automated software updates through Ubuntu's standard apt package manager.Native `.deb` Installation (Recommended)

Installing the official package gives VS Code unrestricted access to system compilers, development SDKs, and global tools, avoiding the file system sandbox and configuration restrictions often encountered with Flatpak or Snap packages.

Open your browser and go to the [official Visual Studio Code Download Page](https://code.visualstudio.com/docs/setup/linux)

Click the `Debian and Ubuntu-based distributions` button to download the installer package for Ubuntu.
* Open your terminal application (Ctrl + Alt + T).
* Navigate to your downloads directory with `cd ~/Downloads`
* Install the package using the following commands: 
    - `sudo apt update`
    - `sudo apt install ./code_*_amd64.deb` -y
    - `sudo apt autoremove`
* Type `Y` to continue installing if needed
* Choose "Yes" to add the Microsoft repository to update VS Code throught apt.
* Type `code` at the prompt to start VS Code. After it starts, give it access to your GitHub account by typing in your password.

(Note: Using `apt` instead of `dpkg` is preferred because it automatically fetches and installs any required system dependencies.

### Install Python Extension in VS Code (citation: Google AI)
To install the Python extension in Visual Studio Code, use the built-in Extensions Marketplace.

Installation Steps
* Start VS Code by typing `code` at the command prompt.
* Open Extensions: click the Extensions icon on the Activity Bar (left side of VS Code) or press Ctrl + Shift + X.
* Search: type "Python" in the top search bar.
* Install: find the official extension by Microsoft (usually the first option) and click `Install` (release). It should look something like "Python (Python language support with extension access...)"

### Clone the `andfn` Repository in VS Code
* In VS Code, choose "Clone Git Repository..."
* In the pulldown menu that requests the repository, either type in the address of the repository (for example, for a username ODLS1 it would be `https://github.com/ODLS1/andfn`), or, if you are logged in to GitHub, wait for VS Code to populate your repositories and choose `andfn` from the pulldown menu.
* For the destination of the repository, create a `Source` directory in your home directory (for example, `/home/odls/Source`)

### Connect your Fork of `andfn` to Toller's "upstream" Version
    cd <local_name_for_repo> [for example, `/home/odls/Source/andfn`]
    git remote add upstream git@github.com:eriktoller/andfn

To update your fork from upstream (which is @eriktoller's `andfn` repository), type:

    git pull --recurse-submodules upstream main

### Install Python Packages
* From the terminal, create a Python "virtual environment" to install the `andfn` dependencies (see the Appendix for some background information about the need for virtual environments on Ubuntu):
    - `cd ~/Source/andfn` [move to the directory containing the `andfn` clone]
    - `mkdir virtual_env` [create a directory for the Python virtual environment]
    - `python3 -m venv virtual_env` [create the virtual environment]
    - `cd virtual_env/bin`
    - `source ./activate` [activate the environment]
    - `./pip install numpy pandas h5py scipy matplotlib pyvista numba pyyaml` [install all the `andfn` dependencies]
    - `./pip install -e /home/odls/Source/andfn` [install the `andfn` package]

### Run "template.py" Example
* Open a terminal from the `Terminal` menu in VS Code 
* Navigate to, for example, `/home/odls/Source/andfn`
* Type `python3 ./examples/template.py` to run the `template.py` example. It should generate an image of four fractures with contour lines.

### Making and committing changes
* Click on the `directory/folder` icon on the top left-hand of the `activity bar` in VS Code (placed in a vertical bar on the left-hand side of VS Code)
* Select a file to edit
* Edit the file and save it
* The changes should now show up under the `source control` icon (also in the `activity bar`) -- click on the icon.
* Click on the changed files to see the differences in the viewer that shows the original file on the left and the changed file on the right.
* Click on the "+" button to stage the files
* Enter a "commit message"
* Click "Commit Changes"
* Click "Synchronize" (or similar, if asked)
* Confirm that changes show up in the GitHub repository

### Using VS Code Artificial Intelligence (AI)
* From the `Help` menu, select `Ask @vscode`
* Ask questions in plain English, setting appropriate context and being specific (it will help guide you with questions and suggestions). For example, ask: "In the andfn Python project currently loaded in VS Code, please suggest a sequence of steps to parallelize the code for better performance".

### Watch Video (if available)
* Download files from Dropbox
* Unzipped `zip` file
* Installed video viewer:
    - `sudo apt install vlc -y`
* Navigate to the location of the video
* Watch video using `vlc video1152107754.mp4`

### Appendix

The following informational message is displayed when trying to install Python packages with `pip`. This is due to Ubuntu's approach to managing the inherent complexity of Python packages.
```
oes:~/Source/andfn(main)$ pip install numpy
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.
    
    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.
    
    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.
    
    See /usr/share/doc/python3.12/README.venv for more information.

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.
```
