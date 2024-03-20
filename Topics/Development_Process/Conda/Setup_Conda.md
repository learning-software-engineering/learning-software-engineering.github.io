# Table of Contents
1. [Miniconda](#Installation-Miniconda)
    - [Miniconda Installation](#Installation-Miniconda)
    - [Setup MacOS for Miniconda](#Setup-MacOS-for-Miniconda)
    - [Setup Windows for Miniconda](#Setup-Windows-for-Miniconda)
2. [Anaconda](#Installation-anaconda)
    - [Anaconda Installation](#Installation_anaconda)
    - [Setup MacOS for Anaconda](#Setup-MacOS-for-Anaconda)
    - [Setup Windows for Miniconda](#Setup-Windows-for-anaconda)
3. [Creating Environments](#Creating-Environments-Python)
4. [Switching Environments](#Switching-Environments-Python)
5. [Removing Environments](#Removing-Environments-Python)
6. [External Resources](#External-Learning-Resources-for-Conda)

# Installation (Miniconda)

With a little bit of navigation, we see that there are download links here: [https://docs.conda.io/projects/miniconda/en/latest/](https://docs.conda.io/projects/miniconda/en/latest/)

So the first step here will just be to download the installer for your system, and then executing it. 

For systems that doesn't have a GUI, you can also use the other installation methods like an installation script provided on the website. 

![conda download page](conda_download.png)

In the picture shown above, download the one that fits your system, in my case, it is the one that says `Miniconda3 macOS Apple M1 64-bit pkg`

Then just download and click through the install process until you have completed. 

The setup guide for **MacOS** is [here](#setup-macos), for **Windows** is [here](#setup-windows)

## Setup [MacOS] for Miniconda

Regarding the setup process for Miniconda, multiple different situations can arise. 

Now, you want to start up the shell of your system and verify if Conda is successfully installed. In my case, MacOS has the default shell being `zsh`, so you can just open up `zsh` by pressing "Command + Space" and typing `terminal`, the first one should be your `shell`. 

Then, after `zsh` appears as a window, type in `conda`, then press enter. 

![verifying conda installation](conda_verify.png)

If you press enter and a bunch of information showed up, then it is likely that conda has successfully installed, and you can proceed directly to the next part [Creating Environments (Python)](#creating-environments-python)

However, if you called conda and nothing seems to have showed up, then it is likely that the installation did not successfully go through. To resolve this issue, depending on your system, there might be different solutions. 

One of the common fixes for this is to call `conda init [shell_type]`. For example, if you are on MacOS, you can follow this guide stated [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html)

![conda init pic](conda_init.png)

With all that being said, we can finally start to unleash the power of Conda. [Hyperlink here](#creating-environments-python)

## Setup [Windows] for Miniconda

> Guide Reference: https://gist.github.com/martinsotir/2bd2e16332dff71e0fa5be3ed3468a6c

Usually in Windows, after you download and installed Miniconda for Windows, it doesn't automatically register in the regular powershell, you will have to carry out a few steps. 

Therefore, you want to first open up `powershell` and do a quick check. 

To do this, you can press the "windows" key, and then search for `powershell`, then press enter to open it, as shown in the picture below.  

![opening powershell](open_powershell.png)

Then, type in `conda`, and press enter, if the following shows up, then you have your installation complete, and you can proceed to the next part [Creating Environments (Python)](#creating-environments-python)

![conda verify windows](conda_verify_windows.png)

If that did not show up, then we will have to proceed into fixing this. 

First, you want to open up an administrator powershell, and type in `set-executionpolicy unrestricted`, then click enter. 

To start up an administrator powershell, simply tap your Windows key, and then type in `Powershell`, then right click and select `Run as administrator`, as shown below. 

![administrator powershell](powershell_administrator.png)

After pressing enter with `set-executionpolicy unrestricted`, you will need to press `A` and then enter, as shown below. 

![execution_policy](execution_policy.png)

Then, you need to press the windows key, and search for `miniconda`, and click on the first one that appears, as shown below. 

![anaconda prompt](anaconda_prompt.png)

In this prompt, type in `conda init powershell`, and press enter. It should show something similar to the following (I already have conda installed, so it should show something a bit different to what I had)

![conda init powershell](conda_init_powershell.png)

After all of these, you should be able to just start up a new `powershell` session, and it should have miniconda installed! With this, you can start to unleash the power of Conda and proceed to the next section!  

## Installation (Anaconda)

You can find the Anaconda installer and detailed installation instructions on their official download page: [https://www.anaconda.com/products/individual](https://www.anaconda.com/download#downloads)

The initial step involves downloading the appropriate installer for your operating system. If you're working on a system without a GUI, you might prefer to use command-line installation methods, which are also detailed on the Anaconda website.

![anaconda download page](anaconda_download.png)

In the screenshot above, select the installer that matches your system. For instance, if you are using a macOS with an M1 chip, you might choose the `Anaconda macOS Apple M1 64-bit pkg`.

Download the installer and follow the prompts to complete the installation process. Make sure you add conda to the environment path during installation 

Here is an example of how the MacOS anaconda installer looks like:
![anaconda installer example] (anaconda_installer.png)

Setup guides for different operating systems can be found through the following links: for **MacOS** [here](#setup-macos-for-Anaconda), and for **Windows**, please follow the same procedure as MacOS, but choose the `64-Bit Graphical Installer (904.4M)` package.

## Setup [MacOS] for Anaconda

The setup process for Anaconda can vary based on your operating system and shell configuration.

To verify if Anaconda has been installed successfully, open your system's shell. For macOS users, the default shell is typically `zsh`. You can open `zsh` by pressing "Command + Space", typing `terminal`, and selecting the first result.

In the terminal window, run the following to display the version of Anaconda installed on your system. 
```
conda list anaconda
```
![verifying anaconda installation](anaconda_verify.png)

If a list of anaconda version appears, it indicates that Anaconda is installed correctly, and you can proceed to [Creating Environments (Python)](#creating-environments-python).

Should you encounter any issues where Anaconda commands are not recognized, one common fix is to initialize Anaconda for your shell. This process can be completed by running `conda init [shell_type]`. If you're using macOS, guidance for this step is provided [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html).

![anaconda init pic](anaconda_init.png)

With Anaconda successfully installed and initialized, you're ready to explore its robust features. You can use the GUI of anaconda or command line.
![anaconda gui](anaconda_gui.png)
[In this doc, we will only talk about creating Python environments using command line](#creating-environments-python). If you need help with GUI, you can check out the official documentation [here](https://docs.anaconda.com/free/navigator/?utm_source=anaconda_navigator&utm_medium=nav-docs).

## Setup [Windows] for Anaconda

The installation and setup process for Anaconda on Windows varies slightly from macOS, but it's designed to be straightforward. Ensuring that Anaconda is added to the PATH during installation is crucial for seamless use of the command line interface.

To verify if Anaconda has been successfully installed on your Windows system, you'll use the Command Prompt or PowerShell. You can open either of these applications by searching for them in the Start menu.

In the Command Prompt or PowerShell, enter the following command to display the version of Anaconda installed on your system.
```
conda list anaconda
```
If you see a list of packages with "anaconda" in their names, it signifies that Anaconda has been installed correctly, and you can move on to [Creating Environments (Python)](#creating-environments-python).

If the `conda` command is not recognized, you might need to add Anaconda to your system's PATH manually or run the initialization command for your shell. This can often be resolved by launching Anaconda Navigator and allowing it to set up everything for you, or by executing the initialization command:

After running this, you may need to restart your Command Prompt or PowerShell to ensure the changes take effect.

This step ensures that the `conda` command is available system-wide, allowing you to manage your Anaconda installation and environments directly from your Command Prompt or PowerShell.

For those who prefer graphical interfaces, Anaconda also provides a GUI called Anaconda Navigator, which can be launched from the Start menu. The official documentation offers comprehensive guides on both command-line and GUI methods for managing your environments and packages. For this document, we'll focus on command-line operations. For GUI assistance, refer to the [official documentation](https://docs.anaconda.com/navigator/).

With Anaconda properly installed and initialized, you're all set to take advantage of its powerful package and environment management capabilities to streamline your Python projects.

# Creating Environments (Python)

Environments in Conda are like separated files in different directories. For example, if you have a Conda environment specifically for Machine Learning projects, when you switch to another software engineering project, you probably want to not use the Machine Learning packages so that they don't interfere with what you're trying to do. 

To do this, open up your shell and type in `conda create -n <name> python=<version>`, where `<name>` is the name of the environment you are creating, and `<version>` is the Python version you want. If you are creating an environment that is not Python, you can also drop the parameter, so that you create an environment with just `conda create -n <name>`. 

In my case, I will create a Python environment with Python 3.11, called "TEST", as shown in the picture below. 

![create environment](anaconda_create_env.png)

What I called here is `conda create -n TEST python=3.11`, and pressed enter. Then, it will ask if you will confirm or not, just type "Y" to confirm and enter. 

Then, you should be able to switch to your new environment that you just created! 

# Switching Environments (Python)

After you have followed the steps above to create multiple environments, you can switch between them easily. 

What you have to do is just call `conda activate <name>`. Where `<name>` is the name of the environment you have created before. 

![conda activate](conda_activate.png)

After you activated, notice that the left most part, it says "(TEST)", which reflects the environment name that I have activated right now. 

If I do anything related to "Python", I will be using the Python under the environment named "TEST". For example, I will invoke `pip list`, which just shows all of the Python packages I have installed on my environment right now. 

![conda pip list](conda_pip_list.png)

As you can tell from the picture above, "TEST" is indeed a fresh installation of Python with no packages installed at all. 

The following is another environment I have, called "ReiBot", and is switched into using `conda activate ReiBot`. 

![conda pip list ReiBot](conda_pip_list_rei.png)

After then, I called `pip list` again, which shows me different list of packages when compared to the environment named "TEST". 

If you want to be more in-depth (working with IDEs), you should be able to find the directory of your Conda environments easily, they should all be stored under the main Conda directory, as shown in the picture below (taken in PyCharm). 

![conda directories](interpreter.png)

# Removing Environments (Python)

After you're done with a specific environment and the project, you can release the environment by calling `conda remove --name <NAME> --all`. 

In my case, I just called `conda remove --name TEST --all`, and proceeded with "Y" and enter. 

This allows me to remove the environment "TEST". 

![conda remove env](conda_env_remove.png)

After everything is done, you should not be able to find the environment named "TEST" anymore. Which means that we have successfully deleted the environment. 

![conda list env](conda_env_list.png)

# External Learning Resources for Conda

1. [**Conda Official Documentation**](https://docs.conda.io/en/latest/): This is the primary source of information about Conda, covering installation, commands, package management, and environment management. 

2. [**Conda Cheat Sheet**](https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html): A quick reference guide provided by the official Conda documentation, summarizing the most common Conda commands and their usage. 
