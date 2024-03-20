# What is Conda and why do you need it? 

Have you ever experienced the frustration when you have multiple Python package conflicts and needs to resolve multiple package dependency issues before you can actually work on a new project? If that's the case, **Conda** is here to save your day!  

Conda is an open-source package management and environment management system that can be used to simplify a lot of the operations regarding environment management. 

This tutorial will focus on using Conda to setup multiple Python environments that can be used for different projects. So that you'll never have to worry about setting up an environment and running into issues again!

# Difference between Anaconda and Miniconda?

As of the time writing, Conda's official website is this: [https://docs.conda.io/en/latest/#](https://docs.conda.io/en/latest/#)

It provides a simple installation method and some general documentation for the usage of Conda. 

However, a quick Google search might tell you that, there's actually two different versions of Conda, one being **Anaconda** and another being **Miniconda**. 

The major difference between **Miniconda** and **Anaconda** is that: 

- Anaconda supports Graphical User Interface (GUI), so you can actually click on things to make it work. 
- Miniconda does not support GUI and is used mainly on the "shell" (e.g. zsh, bash, sh, powershell, etc.) of your system. If you do not know what a "shell" is, this tutorial might be a little bit advanced. 

With all that being said, this tutorial focuses on using Miniconda to setup Conda and multiple Python environments, so you might need to look for another tutorial if you plan to use Anaconda.

# Why do you want to use Conda instead of other environment management solutions? 

Other environment management solutions for Python specifically, includes `pipenv` and `virtualenv`, also support similar functionalities to Conda. 

Each of these solutions all have their own unique strengths and weaknesses, the following is a table that gives an overview to their own capabilities and flaws: 

| Feature | Conda | Pipenv | Virtualenv |
|---------|-------|--------|------------|
| **Cross-Language Support** | Supports multiple languages | Python only | Python only |
| **Environment Management** | Comprehensive environment management | Automates virtual environment management | Isolates Python environments |
| **Package Management** | Manages Python and non-Python packages | Manages Python packages, with `Pipfile.lock` for deterministic builds | Only isolates environments, does not manage packages |
| **Repository** | Large repository (Anaconda Repository) | Uses PyPI | Uses PyPI |
| **Platform Support** | Cross-platform (Windows, macOS, Linux) | Cross-platform | Cross-platform |
| **Simplicity and Intuitiveness** | Can be complex due to additional features | Simpler syntax and intuitive usage | Minimalistic and lightweight |
| **Performance** | Can be slower, especially for large distributions | Can have performance issues with large dependencies | Fast and efficient |
| **Scope** | Suitable for complex, multi-language projects | Ideal for Python-specific development | Focused on Python-only projects |
| **Ease of Setup** | Requires more setup compared to pip | Simplifies setup with automation | Quick and easy setup |

# How do you use Conda?

To actually use Conda, we need to follow the following [general steps](./path/to/your/file.md) to set up