# Learning WSL 2 Usage

## Table of Contents
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Useful Commands](#useful-commands-1)
### [WSL 1 Support](#wsl-1-support-1)
### [Terminology](#terminology-1)
----

## Introduction

**NOTE:** We assume your computer is already virtualization ready with technologies like Hyper-V Threading enabled. If you have a computer which may not obviously satisfy this (remote server, old systems, custom installations), we recommend 1) Enabling virtualization from BIOS/UEFI and then 2) Turning on Hyper-V Windows feature. A simple search with the mentioned keywords would suffice the exact steps.

This article will help Windows users setup and use WSL 2 and save their time solving issues. Before we begin, it is highly recommended to use the modern [Windows Terminal](https://apps.microsoft.com/detail/windows-terminal/9N0DX20HK701?hl=en-us&gl=US) app on Windows for Command Line operations, which allows much more customization and ability to have different types of terminals open at the same time in different tabs (For example, Powershell, Windows Command Prompt and Azure Shell simultaneously).

WSL is a relatively lightweight virtualization tool dedicated for Linux, to run it on top of Windows. It is used by developers not wanting to have a dedicated Linux machine or not wanting to setup dual-boot machines which includes Linux as one of the operating systems. Developers can work and build in Linux environment using WSL on top of Windows, which is also useful when you quickly want to do something in a Linux environment, but it comes with its limitations. The official documentation for WSL by Microsoft can be found [here](https://learn.microsoft.com/en-us/windows/wsl/).

----

## Installation

It is possible to lookup WSL on Microsoft Store or indirectly install WSL by installing a flavor of Linux directly, but such installations have different default settings (precise information is available on official documentation). It is recommended to follow the following steps instead:

The following command will print the available distributions.

    wsl --list --online

Pick a distribution of your choice (Ubuntu is usually a fair choice), and run the following:

    wsl --install <distribution>

If you installed multiple distributions, you can use the following command to set one as default:

    wsl --set-default <distribution>

So, when you just run `wsl`, it will launch that distribution.
To launch specific distribution, run:

    wsl --distribution <distribution>

It's this simple to get started with WSL! We will talk about other settings, features and limitations in the rest of the document.

----

## Useful Commands

### Handling Distributions

To see the state of your local WSL, run:

    wsl --list --all -v

You can see all distributions and their states using this command. To terminate a specific distribution, run:

    wsl --terminate <distribution>

To shutdown WSL and thus all running distributions on it, run:

    wsl --shutdown

To delete a distribution, run:

    wsl --unregister <distribution>

### WSL Help, Update, and Version

To update WSL, run:

    wsl --update

To see WSL version:

    wsl --version

To see possible commands with WSL, run:

    wsl --help

### Distribution Specific Configuration Files

"/etc/wsl.conf" is the configuration file read by WSL in startup when booting the distribution, if it exists. A simple search in the documentation for available configuration options can help automate things when you are launching WSL ! Note that more features have been added in newer builds, so version is important to take care of, which is available [here](https://learn.microsoft.com/en-us/windows/wsl/release-notes).

----

## WSL 1 Support

Microsoft changed the way they parse Windows Path files between WSL 1 and WSL 2, and it created a deadlock where trying to run Docker on WSL 2 will lead to Path errors, and Docker cannot be run on WSL 1 due different virtualization capabilities. There is no visible solution to the author's best knowledge and extensive research to bypass setup scripts involved. It is recommended to use Docker only on Linux instead, especially for the sake of best compatibility.  Thus, we are going to discuss how to run WSL 1 for any similar reasons that may require it.

Following the installation steps in this document, it is assumed by WSL that the user wants to use the latest version, version 2. To change this default setting, run:

    wsl --set-default-version 1

To change the version of a specific distribution instead, run:

    wsl --set-version <distribution> <version>

This allows backwards compatibility. To change WSL 1 distribution launch settings:

1) Run regedit.exe
2) Navigate to HKCU\Software\Microsoft\Windows\CurrentVersion\Lxss
3) Use [WSL_DISTRIBUTION_FLAGS](https://learn.microsoft.com/en-us/windows/win32/api/wslapi/ne-wslapi-wsl_distribution_flags) to change launch settings for distributions. For example, 0x7 implies all flags are enabled (7 = 1 + 2 + 4).

**NOTE:** Modifying registers can potentially damage and crash you system and data. It is important to be responsible and think twice before implementing changes.

This information should be mostly sufficient, and further information is available on official documentation.

----

## Terminology
- [**Virtualization**](https://www.ibm.com/topics/virtualization): the action of creating an abstraction layer over computer hardware that allows the hardware elements of a single computer like processors, memory, storage and more to be divided into multiple virtual computers, commonly called virtual machines (VMs). This action allows you to run Linux on top of Windows without shutting it down!

- **Distribution**: The operating system being virtualized on your Windows machine, usually some flavor of Linux.
