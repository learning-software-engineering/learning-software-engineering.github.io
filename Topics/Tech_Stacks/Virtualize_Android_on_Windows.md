
# Virtualize Android on a Windows Device

## Table of contents
### [Introduction](#introduction-1)
### [What is virtualization](#what-is-virtualization-1)
### [Virtualizing an Windows machine to an Android device](#virtualizing-an-windows-machine-to-an-android-device-1)
### [Install an APK file on the virtualized windows device](#install-an-apk-file-on-the-virtualized-windows-device-1)
### [Additional Resources](#additional-resources-1)

## Introduction

Device consistency is often a good condition for programmer, especially the software developer, to maintain their train of thoughts. Specifically, it is easier to focus on the logic and flow of development when there's no distraction caused by constant changing of devices. In other words, if a software developer is constantly changing working environments, for example, coding on Macbook, but testing on an iPhone, it would be more error-prone since the sudden change of work space might derail the programmer's thoughts.
Therefore, it would be more efficient if the software developer can design, code, and test on a same device, which is not often the case since there are development requirements across all sorts of operating systems. One functionality that modern laptop support to solve this problem is the technique of virtualization, that is virtualize the laptop and pretend it is running as an phone or other computer. In this note, I will show a specific virtualization branch: virtualizing a Windows computer as an Android phone.

## What is virtualization

Virtualization is the process of creating a virtual version of something, such as a virtual machine, operating system, storage device, or network resource, that operates independently of its physical counterpart. In computing, virtualization enables multiple operating systems to run on a single physical machine, allowing for greater efficiency, flexibility, and cost savings.

Virtualization creates a layer of abstraction between the physical hardware and the operating system, applications, or other resources that run on it. This allows multiple virtual machines, each with its own operating system and applications, to run on a single physical server, which can save on hardware costs, power consumption, and data center space.

Virtualization can also be used to create virtual networks, storage devices, and other resources, which can be accessed by multiple users or applications. Virtualization technology has revolutionized the way that IT infrastructure is designed and managed, making it easier and more efficient to deploy and manage complex systems.

## Virtualizing an Windows machine to an Android device

To virtualize an Windows machine to an Android device, follow the following steps:
1. Check the virtualization availability on your windows device <br />
  i) Even though for most modern windows computers, the virtualization functionality is auto-enabled, but it is still a good practice to double check. To do so:<br />
     a. Go to **task manager** <br />
     b. Go to **performance** section <br />
     c. Click on **CPU** <br />
     d. Check whether virtualization is enabled. <br />
     e.g.: <br />
     ![image](https://user-images.githubusercontent.com/74875627/226499401-fde43338-106a-400b-9496-479f09403731.png)!  <br />
     e. In case it is not enabled, you have to enable it from the BIOS/UEFI interface.
  ii) Enable the **Virtual Machine Platform** feature. To do so:<br />
     a. Go to the **Turn Windows features on or off** in control panel by search.  <br />
     b. Inside it, check the Virtual Machine Platform checkbox. e.g.: <br />
     ![image](https://user-images.githubusercontent.com/74875627/226499848-2a9d7f23-f254-4554-8fa7-e7d0bda891d6.png)  <br />
     c. Restart the PC if necessary to make sure the change is executed.
  iii) Install the windows subsystem for android from the Microsoft store from the following link:   <br />
     a. [Windows subsystem for android download](https://apps.microsoft.com/store/detail/windows-subsystem-for-android%E2%84%A2-with-amazon-appstore/9P3395VX91NR?hl=en-us&gl=us) <br />
     b. After installation, open the windows subsystem for android <br />
     c. Go to the **Developer** section. <br />
     d. Enable the **Developer mode**  <br />
     e. Click **Manage developer setting** to connect with local IP. <br />
  iv) You are done! After the windows subsystem is running normally, your Windows device is pretending itself to be an Android phone, so that you can do various functionalities that is available on Android. <br />

### Install an APK file on the virtualized windows device
  i) Even though your windows device has already been virtualized as an Android device, and you can run an Android app, you still need additional support to install APK files, that is short for **Android Package Kit**<br />
  ii) To install APK files, follow <br />
      a. Download the newest version of WSA Packman from this link: [WSA Packman download](https://github.com/alesimula/wsa_pacman/releases/tag/v1.4.0).<br />
      b. Install it following default settings.<br />
      c. Make sure the windows subsystem is running on the background <br />
      d. Open WSA PackMan and wait until it shows **connected** <br />
      e. Then, you are good to download any APK files on your device! <br />

## Additional Resources

* Source repository for WSA Packman [WSA Packman repository](https://github.com/alesimula/wsa_pacman) <br />
* To watch a detailed tutorial, go to [Install APK file on windows tutorial](https://www.youtube.com/watch?v=D_AiqB-eVig&t=77s)
