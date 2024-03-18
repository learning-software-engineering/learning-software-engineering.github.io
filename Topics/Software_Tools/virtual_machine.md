# What are Virtual Machines?

A virtual machine, or VM, resembles a physical computer in terms of components such as CPU, memory, and storage. However, unlike traditional hardware, VMs exist as software-defined entities within physical servers, functioning through code rather than tangible hardware[^1].

Virtualization involves creating a virtual computer with allocated CPU, memory, and storage resources, drawn from a physical host computer or a remote server. A VM operates as a computer file or image, emulating the behavior of a real computer. It can run within a window as an independent computing environment, facilitating tasks such as running different operating systems. A VM operates in isolation from the host system, ensuring that the software within the VM does not interfere with the primary operating system of the host computer[^1].

For example, if you own a Windows computer, but are required to develop in a Linux environment, you can utilize a VM to operate as your Linux machine, without having to purchase one physically.

# Getting Started with Virtual Machines

For this tutorial, I will be using VirtualBox for Windows, and will be installing a Linux Xubuntu VM. The step-by-step instructions are from The Odin Project's guide to VM installation[^2].

1. Download VirtualBox for Windows from [here](https://www.virtualbox.org/wiki/Downloads) [^3].
2. Install VirtualBox by opening the downloaded file from step 1, and follow the installation instructions from the setup window.
3. Download the Xubuntu distribution of Linux from [here](https://mirror.us.leaseweb.net/ubuntu-cdimage/xubuntu/releases/22.04/release/) [^4]. Make sure to download the file ending with `.iso`.
4. Open the now Installed VirtualBox application from step 2, and click on the New button. This will allow you to create a virtual operating system, which you should call Xubuntu. Make sure that you have 30 GB in reserve for this process. In the ISO Image option, pick Other, and choose the Xubuntu ISO file you installed in Step 3. 
5. Next, you will need to set up your username and password as desired for your VM. Make sure to select the Install in Background option as well.
6. Now, you will need to setup the hardware. Ideally, you want to set the Base Memory to half of your total RAM, but a minimum of 2048 MB works as well [^2].
7. Next, you will be asked to set the Disk Size for the VM, which you want to be at least 30 GB.
8. After step 7, you should be taken to a Summary page, where you can go ahead and click Finish to start the installation process.
9. Once it is installed, click the green 'Show' arrow at the top. You will be asked to log in with the username and password set up in step 5, and you will need to do a bit more configuration.
10. Once that is complete, the green 'Show' arrow will most likely have turned into a green 'Start' arrow. Click on that, and you are ready to use your new Linux Xubuntu VM!

# Sources:
[^1]: [What is a virtual machine (VM)?](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-a-virtual-machine)
[^2]: [The Odin Project](https://www.theodinproject.com/lessons/foundations-installations)
[^3]: [Virtual Box Install Link](https://www.virtualbox.org/wiki/Downloads)
[^4]: [Xubuntu Install Link](https://mirror.us.leaseweb.net/ubuntu-cdimage/xubuntu/releases/22.04/release/)
