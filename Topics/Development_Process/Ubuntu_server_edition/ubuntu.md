# Guide for setting up a home server with Ubuntu Server Edition

## Introduction
If you ever developed a discord bot, you might wonder how things just work as long as we have either Python or javascript files running on our computer. That is because either Python or JavaScript program is serving as the backend of the discord bot, and this also shows us that any computer can be used as a server.  

Thus instead of paying for cloud services such as AWS, turning a spare computer into a web server might be already enough for development purposes. Not only can you save the cost, but this also gives you some invaluable experience in server administration. In this guide, I will be showing how this can be done with the Ubuntu server edition, a popular and well-supported distro, and a piece of minimum hardware- a Raspberry Pi 4b.

## Requirements

Before we hop into the setup, we need to make sure we have everything we need: The device, ethernet access or WLAN which we also need access to the router setting.

## About Ubuntu Server LTS 20.04
Ubuntu is a famous Linux distribution based on Debian. Unlike the standard edition which comes with a display manager, desktop environment, and daily software such as LibreOffice, the server edition comes with minimum installation, only stuff like apache2 which is needed to run a minimum server. It will be a very different experience if one works only in a desktop environment since we will be working in ttys(teletypewriter, but take it for a terminal for simplicity) most of the time.
![Alt text](Assets/IMG_20240315_021624_8542.jpg)

## Installation of the OS

Depending on the device, there are two usual options. If it is something with the architecture of x86_64, one can download and flash the image to a drive and then live boot it into the target device, following the instructions to install it. Or if it is arm like I did on my rpi4b, the image needs to be flashed into the SD card and there is the option of pre-installed ones. 

## Connection to Internet
The very first task that needs to be completed after the installation of the system is to connect to the Internet. And by connecting to the Internet I mean two-way: both that the device can access the Internet and accessed from the Internet.  

Let's begin with accessing the Internet. There are two options as well, either ethernet cable or WLAN. The second one is the tricky one, as there is no for example a button you can click on and a graphic Interface where you can see all the SSIDs and just input the password. The default way to connect wirelessly is a tool so-called "netplan" and the configuration is located at `/etc/Netplan/` where we can see a YAML file. Use `sudo nano <xxx.yaml>` to edit it in the following format:

```
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    version: 2
    wifis:
        wlan0:
            optional: true
            access-points:
                "BELL309":
                    password: "14717219F1E1"
            dhcp4: true  

```
replace "BELL309" with the actual SSID and password as the corresponding password. press `ctrl+o` and `ctrl+x` to save and exit nano. After that `sudo netplan -debug generate` to check if there is any syntax error in the yaml. After verification is done `sudo reboot` to reboot. After reboot, the system shall automatically connect to the WLAN. use `ip a` or `ping google.com` to verify.  

Great, next, as a server, we also need to make sure that the device is accessible from the Internet. This requires port forwarding from the router.
In the browser of another computer, log into the router through its private IP address in the local area network. 
![Alt text](Assets/port.png)
Then in "Port forwarding", select the device either from the device name or local IP address(192.168.x.x) and set up a few port forwarding rules we need. For example, 22 for SSH, 80 for HTTP, and 443 for HTTPS. After saving the configuration, we can try accessing the global IP of the router on a browser(You can figure this one out quickly by googling "ip" on any other device connected to the same network) like the following: 
![Alt text](Assets/image.png)
If you can see such a page, congratulations, your server is now also accessible from the Internet.
## Installation of necessary tools using apt

After making sure that the device can access the internet, the next step is to install the packages we need. The easiest way to do that in a tty is to use the package manager.
```
$ sudo apt update
$ sudo apt install openssh-server
$ sudo apt install git
...(any other tools you need for your development purpose, like nodejs)
```

## SSH
In order for ssh to work, we need to first enable it. After installing the package which should automatically enable the service as in the previous step, `sudo systemctl status ssh` to double check. If it's blocked by UFW, `sudo ufw allow ssh`.  

To ssh from another device, in the other device's terminal
`ssh <username>@<ip address of the router>` like this:  

![Alt text](Assets/ssh.png)
and work the same way as in tty but copy-pasting would be much more convenient since on the host device there is only a terminal-based browser and no cursor.

## Web Server Example

As a server, it needs to serve something. The most common thing to serve would be a web app. For example, I have a web app running in a docker and listening on port 4000 on this device, while port forwarding directly from 80 to 4000 on the router would technically work, it is recommended to have a web server that does the reverse proxy. Let's take nginx for example, detailed setup of nginx can be found here: https://learning-software-engineering.github.io/Topics/Development_Process/Nginx.html. After Nginx is up with a valid SSL certificate, the web app would become available to the Internet over an IP address or a domain(which requires DNS setup in both the domain provider and nginx).  

![Alt text](Assets/nginx.png)

![Alt text](Assets/invidious.png)
## Further reading
#### nginx
https://learning-software-engineering.github.io/Topics/Development_Process/Nginx.html

#### Obtaining SSL certificates using certbot

https://certbot.eff.org/pages/about

#### DuckDNS to deal with dynamic DNS

https://learning-software-engineering.github.io/Topics/Development_Process/Duckdns.html

#### Full Ubuntu 20.04 Server Documentation

https://assets.ubuntu.com/v1/544d9904-ubuntu-server-guide-2024-01-22.pdf

