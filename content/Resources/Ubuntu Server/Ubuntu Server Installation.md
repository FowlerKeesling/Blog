---
publish: true
---
>**Themes:** [[Data Ownership]], [[Server]]
>**Status:** [[Sprouts|🌱]] 
>**Tags:** #Resource

# Introduction
This server will be built using Ubuntu Server, a Linux distribution. Ubuntu Server is an operating system, just like Windows or Mac OS. However unlike Windows or Mac OS, Ubuntu Server does not have a graphical user interface. Most administration is done from the command line using terminal commands.. This can be intimidating for someone who has always used graphical interfaces, but I will cover the basics as best as I can. With a little patience and practice, you'll likely find that working from the terminal is much easier than it first appears.

# Instructions
>[!info] Primary Computer
>In the initial stages of this project, you will be jumping from your primary computer to your server computer a lot. I will indicate using callouts like these what computer should be used when following the steps that are listed below.

## Download the Required Tools:

1. [Ubuntu Server](https://ubuntu.com/download/server)
2. [Balena Etcher](https://etcher.balena.io/) 

## Flash the Ubuntu Server ISO onto the USB:

1. Open Balena Etcher
2. Select the Ubuntu Server ISO
3. Select the USB flash drive
4. Create a bootable USB flash drive
5. Eject the USB drive safely

>[!info] Server Computer

## Install Ubuntu Server:

1. Insert the USB flash drive into the server computer while the computer is turned off
2. Connect the USB keyboard and the external monitor to the server computer
3. Open the server computer's BIOS or UEFI settings (search how to do this for your specific model of computer)
4. Select the USB flash drive as the temporary boot device, then continue booting
5. Start the installation

## Configure Ubuntu Server:

During installation, accept the default options except for the following:
- Disable LVM
- Enable OpenSSH Server

When the installation is done, document the following in the [[Server Administration|Server Administration Notes]]
- Name
- Server name
- Username
- Password
- Server IPv4 address

## Login Remotely:

>[!info] Pimary Computer

1. Open the terminal application
2. Run the following command
	- Replace **username** with the username you created during installation
	- Replace **server-IPv4** with the server's IPv4

```bash
ssh username@server-IPv4  
```

>[!todo] Command Breakdown
>For those of you unfamiliar with Linux terminal commands. I will do my best to break down each new command as I go. This way you will be able to learn as you follow.
>
>**SSH:** SSH stands for Secure Shell. It is a protocol used to securely connect to another computer over a network.
>
>**IPv4:** This is your server's address, just like a home address, this information is used to direct you to the right computer.

3. Enter the password you created during installation
4. Update the software using the following commands

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

>[!todo] Command Breakdown
>**sudo:** Sudo tells the computer that you will be running the command using administrative privileges. It is an abbreviation for "superuser do".
>
>**apt:** Apt stands for "Advanced Package Tool". It is used for managing software packages.
>
>**update:** Update downloads the latest list of available software packages from the configured repositories.
>
>**upgrade:** Upgrade installs the available updates for software already installed on the system.

5. Reboot the server computer

```bash
sudo reboot
```

6. Close the terminal
# Back Matter
---
Parent Page: [[Home Server Build Guide]]
Next Step: [[Visual Studio Code Installation]]
Previous Step: [[Home Server Hardware Requirements]]