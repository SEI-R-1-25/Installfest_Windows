# Windows InstallFest

![LinuxVWindows](https://www.psychz.net/content/apr13/windows-vs-linux.png)

## Overview

We'll be installing all of the tools necessary to develop applications on a windows machine running a linux environment/linux machine.

For windows users, you'll be utilizing a built in feature called WSL2 or windows subsystem for linux.

**Windows users, you'll have sections that pertain specifically to your machine.** For example `Section 1 (Windows)`

## Objectives

- Install WSL2 (Windows)
- Install Zsh and Oh-My-Zsh
- Install NodeJS
- Install Python3
- Install Heroku
- Install Postgres
- Install MongoDB
- Install Git

## Installing WSL (Windows)

Open `powershell` as an **`admin`**. Once powershell opens, run the following within that shell:

```ps
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

**NOTE**: In order to install WSL2, your machine must meet the following requirements:

> - For x64 systems: Version 1903 or higher, with Build 18362 or higher.
> - For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.
> - Builds lower than 18362 do not support WSL 2. Use the Windows Update Assistant to update your version of Windows.

Now we'll enable the virtual machine feature in your machine, WSL runs in a virtual environment, it's like running a computer inside of another computer!

Enter the following in `powershell` with **`admin`** privileges:

```ps
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**At this point, you must restart your machine!**

### Installing The Linux Kernal Update Package

Install the following package from this **[LINK](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)**

It's safe I promise!

Open `powershell` again with **`admin`** privileges and enter the following:

```ps
wsl --set-default-version 2
```

Let's install our linux distribution, we recommend Ubuntu 18.04 which you can download from this **[LINK](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)**. It will take you directly to the microsoft store.

Here's a list of all supported distributions:

- Ubuntu 16.04 LTS
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- openSUSE Leap 15.1
- SUSE Linux Enterprise Server 12 SP5
- SUSE Linux Enterprise Server 15 SP1
- Kali Linux
- Debian GNU/Linux
- Fedora Remix for WSL
- Pengwin
- Pengwin Enterprise
- Alpine WSL

Once you reach the Microsoft store, click the `Get` button to download and install Ubuntu 18.04.

Once the download completes, you should be prompted with a terminal window:

![Bash](https://docs.microsoft.com/en-us/windows/wsl/media/ubuntuinstall.png)

Enter a username and password, we recommend setting these the same as your windows os login!

Now let's ensure that the Ubuntu environment is on WSL2, enter the following into `powershell` as an **`admin`**:

```ps
wsl --list --verbose
```

From the list given, find the Ubuntu instance and add the information to the next command:

```ps
wsl --set-version <distribution name> <versionNumber>
```

Once these steps are completed, you should be able to open your Ubuntu environment, by selecting it from your start menu, we recommend pinning it to your taskbar. Keep the Ubuntu terminal open for the remainder of this walkthrough.

### Optional (Windows)

You can download the new windows terminal **[HERE](https://docs.microsoft.com/en-us/windows/terminal/get-started)**.

## Updating The Linux Environment

Before proceeding, run the following command in your terminal or Ubuntu for windows users:

```sh
sudo apt update
```

## Installing Git

Git is a version control manager that we'll be utilizing throughout this program. Install it by entering the following command into your terminal:

```sh
sudo apt-get install git
```

Let's configure Git.

Enter the next commands into your terminal:

```sh
git config --global user.name "Your Name"
```

Replace your `Your Name` with your name from Github.

```sh
git config --global user.email "youremail@domain.com"
```

Replace `youremail@domain.com` with the email you have registered with Github.

### Setting Up Our Github SSH Keys

Ssh keys are used to identify machines/users via an encoded key.

To create a ssh key, enter the following command in your terminal:

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**NOTE**: Be sure to replace `your_email@example.com` with your email that you have registered with Github.

When you're prompted to `Enter a file in which to save the key,` press Enter. This accepts the default file location.

When prompted for a password, hit the enter key twice to skip this step:

```sh
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

We'll now start the ssh agent, enter the following into your terminal:

```sh
eval "$(ssh-agent -s)"
```

Now enter the following into your terminal:

```sh
ssh-add ~/.ssh/id_rsa.pub
```

Now let's install `xclip`. `xclip` is used so that we can copy items into our clipboard, enter the following into your terminal:

```sh
sudo apt-get install xclip
```

Now we can copy our ssh key:

```sh
xclip -selection clipboard < ~/.ssh/id_rsa.pub
```

Follow the steps outlined **[HERE](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)** starting from step 2, we've already completed step 1.

## Installing Zsh and Oh-My-Zsh

### Installing Zsh

Zsh is an extension of the regular bash shell that many computers use as default. It provides us with features that the regular bash shell does not have.

Install Zsh by running the following command in your terminal:

```sh
sudo apt install zsh -y
```

### Installing Oh-My-Zsh

Oh-My-Zsh is an extension of the Zsh prompt. It provides us with useful information in a clear and legible format.

Install Oh-My-Zsh by running the following command in your terminal:

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

A prompt will appear to ask if you want to switch your shell to Zsh, select `yes`.

Close your terminal and re-open it, Oh-My-Zsh should load by default.

## Installing VsCode

VsCode is going to be our text editor of choice for this course.

You can download it **[HERE](https://code.visualstudio.com/download)**

Once downloaded, go ahead and run the installer. Once the installer completes, open VsCode.

### Installing The WSL Remote Extension (Windows)

Once you open VsCode, you may be prompted to install the Remote WSL Extension. Go ahead and do so. If you are not prompted, you can download it **[HERE](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)**.

## Installing NodeJS

NodeJS is a runtime environment that allows us to run javascript outside of a browser.

To install NodeJS, run the following command in your terminal:

```sh
sudo apt install nodejs
```

Confirm the installation with the following command:

```sh
nodejs --version
```

## Installing Python3

We'll be learning the Python language later on in this course.

To install Python3, enter the following command in your terminal:

```sh
sudo apt install python3 python3-pip ipython3
```

Confirm the installation with the following command:

```sh
python3 --version
```

## Installing Heroku

Heroku is a web hosting service that we'll be utilizing to deploy our projects throughout the course.

Enter the following command in your terminal to install the heroku cli:

```sh
curl https://cli-assets.heroku.com/install.sh | sh
```

### Installing Npm

Npm is a package manager for node, it will allow us to install 3rd party packages throughout the course.

To install npm, run the following command in your terminal:

```sh
sudo apt install npm
```

Confirm the installation with the following command:

```sh
npm --version
```

## Installing PostgreSQL

PostgreSQL is going to be our relational database of choice for this course. Install it by running the following command in your terminal:

```sh
sudo apt install postgresql postgresql-contrib
```

Once the installation completes, run the next command in your terminal to confirm the installation:

```sh
psql --version
```

To start the postgres service, enter the following command in your terminal:

```sh
sudo service postgresql start
```

Once postgres starts, enter the following in your terminal:

```sh
createdb `whoami`
```

## Installing MongoDB

MongoDB is a document based database that we'll be using throughout this course. Enter the following into your terminal to install MongoDB:

```sh
sudo apt-get install mongodb
```

Confirm the installation with the following command:

```sh
mongod --version
```

## Resources
