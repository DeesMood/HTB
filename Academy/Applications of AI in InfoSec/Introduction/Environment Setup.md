[Hack The Box - Academy](https://academy.hackthebox.com/module/292/section/3290)
## The Playground
The first is The Playground. Because we acknowledge that not everyone will have the computer resources required to build the models in this module, we have provided a Virtual Playground Environment for you to use if you absolutely need it.

Because this is separate from PwnBox, there are specific sections where you can spawn this VM. You can connect to it using your HTB VPN profile or PwnBox. The VM exposes Jupyter for you to work in, which will be covered in the next section, but you can access it on `http://<VM-IP>:8888`. You can spawn the VM and extend instance time if needed at the bottom of this section or any of the `Model Evaluation` sections in the module.
## Miniconda
### Why Miniconda?

You might wonder why we use `Miniconda` instead of a standard `Python` installation. Here are a few compelling reasons:

- `Performance:` `Miniconda` often performs data science and machine learning tasks better due to optimized packages and libraries.
- `Package Management:` The `Conda` package manager simplifies package installation and management, ensuring compatibility and resolving dependencies. This is particularly crucial in deep learning, where projects often rely on a complex web of interconnected libraries.
- `Environment Isolation:` `Miniconda` allows you to create isolated environments for different projects. This prevents conflicts between packages and ensures each project has its dedicated dependencies.
## Installing Miniconda
### Windows

While the traditional installer works well, we can streamline the process on Windows using `Scoop`, a command-line installer for Windows. `Scoop` simplifies the installation and management of various applications, including `Miniconda`.

First, install `Scoop`. Open PowerShell and run:

  Environment Setup

```powershell-session
C:\> Set-ExecutionPolicy RemoteSigned -scope CurrentUser # Allow scripts to run
C:\> irm get.scoop.sh | iex
```
Next, add the `extras` bucket, which contains `Miniconda`:

  Environment Setup

```powershell-session
C:\> scoop bucket add extras
```

Finally, install `Miniconda` with:

  Environment Setup

```powershell-session
C:\> scoop install miniconda3
```

This command installs the latest Python 3 version of `Miniconda`.

To verify the installation, close and reopen PowerShell. Type `conda --version` to check if `Miniconda` is installed correctly.

  Environment Setup

```powershell-session
C:\> conda --version

conda 24.9.2
```

### MacOS

Homebrew, a popular package manager for macOS, simplifies software installation and keeps it up-to-date. It also provides a convenient way for macOS users to install Miniconda.

If you don't have `Homebrew`, install it first by pasting the following command in your terminal:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once `Homebrew` is set up, you can install `Miniconda` with this simple command:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ brew install --cask miniconda
```

This command installs the latest version of `Miniconda` with Python 3.

To verify the installation, close and reopen your terminal. Type `conda --version` to confirm that `Miniconda` is installed correctly.

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda --version

conda 24.9.2
```
### Linux

Miniconda provides a straightforward installation process that relies not solely on a distribution’s package manager. You can obtain the latest Miniconda installer directly from the official repository, run it silently, and then load the conda environment for your user shell. This approach ensures that conda commands and environments are readily available without manual configuration.

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
JustSomeRedTeamer@htb[/htb]$ chmod +x Miniconda3-latest-Linux-x86_64.sh
JustSomeRedTeamer@htb[/htb]$ ./Miniconda3-latest-Linux-x86_64.sh -b -u
JustSomeRedTeamer@htb[/htb]$ eval "$(/home/$USER/miniconda3/bin/conda shell.$(ps -p $$ -o comm=) hook)"
```

Confirm that Miniconda is installed correctly by running:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda --version

conda 24.9.2
```
## Init
The `init` command configures your shell to recognize and utilize `conda`. This step is essential for:

- `Activating environments:` Allows you to use `conda activate` to switch between environments.
- `Using conda commands:` Ensures that `conda` commands are available in your shell.

To initialize `conda` for your shell, run the following command after installing `Miniconda`:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda init
```

This command will modify your shell configuration files (e.g., `.bashrc` or `.zshrc`) to include the necessary `conda` settings. You might need to close and reopen your terminal for the changes to take effect.

Finally, run these two commands to complete the `init` process

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda config --add channels defaults
JustSomeRedTeamer@htb[/htb]$ conda config --add channels conda-forge
JustSomeRedTeamer@htb[/htb]$ conda config --add channels nvidia # only needed if you are on a PC that has a nvidia gpu
JustSomeRedTeamer@htb[/htb]$ conda config --add channels pytorch
JustSomeRedTeamer@htb[/htb]$ conda config --set channel_priority strict
```
## Deactivating Base
After installing `Miniconda`, you'll notice that the `base` environment is activated by default every time you open a new terminal. This is indicated by the `(base)` prefix on your path.

  Environment Setup

```shell-session
(base) $ 
```

While this can be useful, it's often preferable to start with a clean slate and activate environments only when needed. Personally, I wouldn't say I like seeing the `(base)` prefix all the time, either.

To prevent the `base` environment from activating automatically, you can use the following command:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda config --set auto_activate_base false
```

This command modifies the `condarc` configuration file and disables the automatic activation of the `base` environment.

When you open a new terminal, you won't see the `(base)` prefix in your prompt anymore.

## Managing Virtual Environments
They are critical for AI tasks for a few reasons:

- `Dependency Isolation:` Each project can have its own set of dependencies, even if they conflict with those of other projects.
- `Clean Project Structure:` Keeps your project directory clean and organized by containing all dependencies within the environment.
- `Reproducibility:` Ensures that your project can be easily reproduced on different systems with the same dependencies.
- `System Stability:` Prevents conflicts with your global Python installation and avoids breaking other projects.
## Essential Setup
With your `Miniconda` environment set up, you can install the essential packages for your AI journey. These packages generally cover what will be needed in this module.

While `conda` provides a broad range of packages through its curated channels, it may not include every tool you require. In such cases, you can still use `pip` within the `conda` environment. This approach ensures you can install any additional packages that `conda` does not cover.

Use the `conda install` command to install the following core packages:

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda install -y numpy scipy pandas scikit-learn matplotlib seaborn transformers datasets tokenizers accelerate evaluate optimum huggingface_hub nltk category_encoders
JustSomeRedTeamer@htb[/htb]$ conda install -y pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia
JustSomeRedTeamer@htb[/htb]$ pip install requests requests_toolbelt
```
## Updates
`conda` provides a method to keep conda-managed packages up to date. Running the following command updates all conda-installed packages within the `(ai)` environment, but it does not update packages installed with `pip`. Any pip-installed packages must be managed separately, and mixing `pip` and `conda` installations may increase the risk of dependency conflicts.

  Environment Setup

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda update --all
```

