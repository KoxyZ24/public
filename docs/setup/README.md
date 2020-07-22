# Setup

## Introduction

Our programming exercises require a Unix-like OS (operating system), in particular GNU/Linux.

There are several ways to get a working Linux environment :

- Buy a computer which comes with Linux pre-installed
- Install Linux yourself
  - Natively
    - In dual-boot, which allows you to choose between Windows and Linux when your computer starts
    - In replacement of any existing OS
  - Virtualized
    - Using a third-party hypervisor (VirtualBox)
    - Using the Windows Subsystem for Linux

This document focuses on the latest method : "Windows Subsystem for Linux".

## Install Windows 10

Skip this part if Windows 10 is up-to-date.

### Download

- Visit https://www.microsoft.com/en-us/software-download/windows10ISO (if you already are on Windows, you might need to modify the user-agent)
- Select "Windows 10" edition
- Confirm
- Select "English" product language
- Confirm
- Click on "64-bit Download" button

### Install

- Burn on flash drive (using Rufus https://rufus.ie is advised)
- Boot on the flash drive
- If you see "Press any key to boot from CD or DVD..." do it immediately
- This tutorial is using Windows 10 Home
- The system will reboot several times

#### Wait for Windows 10 to be idle

- Open the Task Manager (right-click in Taskbar or use the shortcut <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Esc</kbd>)
- Click on "More details"
- Select "Performance" tab
- Wait for all the graphs to be completely steady (especially CPU, Wi-Fi, Ethernet)
- Reboot
- Repeat [Wait for Windows 10 to be idle](#wait-for-windows-10-to-be-idle) until the system is idle shortly after startup

#### Install Updates

- Click on :
  - Start
  - Settings
  - Update & Security
  - Check for updates (even if it says "No updates are available")
- Wait until every component Status is "Pending restart"
- Click on "Restart now"
- Repeat [Install Updates](#install-updates) until you see "You're up to date"

## Install a web browser

Skip this part if you have a modern & full-featured web browser (e.g. Chrome, Firefox, etc).

We recommend to use Firefox with the extension "uBlock Origin" and the additional filters lists :

- Annoyances
  - EasyList Cookie
  - uBlock filters - Annoyances

Make sure to apply changes.

## Install Linux

Skip this part if you already have WSL with Debian (or similar system e.g. Ubuntu).

### Install Windows Subsystem for Linux (WSL2)

Follow the guide : https://docs.microsoft.com/en-us/windows/wsl/install-win10 \
To "Open PowerShell as Administrator", right-click on the Start menu.

### Install Debian

- Visit https://www.microsoft.com/en-us/p/debian/9msvkqc78pk6
- Click on "Get" button
- Launch
- Create user as requested (the password doesn't need to be secure and you have to remember it)
- Leave (by using the shortcut <kbd>Ctrl</kbd>+<kbd>D</kbd>, closing the window or typing the `exit` command)

## Install VSCode

Download it from the [official website](https://code.visualstudio.com).
Run the installer, check all "Additional Tasks".

### Install remote extension

Launch VSCode, once started it should detect WSL and propose you to install the "Remote - WSL" extension, which is needed for the next steps.

## Configure Linux

### Connect to remote WSL

Click on the bottom-left green button (overlay says "Open a remote window"), select "Remote-WSL: New Window".

It will open a new VSCode window then install and run a server program in Linux to help VSCode running in its context.

The bottom-left green button (Remote Host) in the VSCode status bar should now indicate "WSL: Debian".

You can close the previous VSCode window.

### Configure tools

In the Menu Bar of VSCode, click on "Terminal", then "New Terminal".

A new panel should appear looking like :

```
user@DESKTOP-XXXXXXX:~$ █
```

This is a command-line interface, you can type commands and execute them pressing <kbd>Enter</kbd>. You can also complete your command using <kbd>Tab ↹</kbd>. For instance type "`ec`" :

```
user@DESKTOP-XXXXXXX:~$ ec█
```

Then press <kbd>Tab ↹</kbd>. The command will be completed to "`echo`" and a space is added, waiting for arguments to be provided, type "`Hello World`" then <kbd>Enter</kbd> :

```
user@DESKTOP-XXXXXXX:~$ echo Hello World
Hello World
user@DESKTOP-XXXXXXX:~$ █
```

`echo` is a program that displays text. Now you will execute commands that will install all the necessary programs you will need :

```
sudo apt update
```

Type the password you entered during [Linux installation](#install-debian).
When it's over (the command prompt appears again), continue entering commands (we hide their output):

```
sudo apt -y upgrade
sudo apt -y install curl
curl https://raw.githubusercontent.com/01-edu/public/master/docs/setup/configure.sh | bash
```

Copy the last line (`ssh-ed25519...`) then :

- Connect to Gitea (https://git.DOMAIN where DOMAIN is the 01 platform address)
- Click on top-right menu "Profile and Settings..."
- Click on "Settings"
- Go to "SSH / GPG Keys" tab
- Click on "Add Key" button in "Manage SSH Keys" section
- Paste the public key in the "Content" text area (the "Key Name" will be automatically set)
- Click on "Add Key"

Now you are able to push & pull code to Gitea using `git`.