# Set up your system after a fresh arch linux install

## Overview

This guide helps you in the process of setting up an Arch Linux after a fresh install. We're going to take care of a few key components:

- **Setting up a user**

- **Display Renderer:** Xorg 
- **Display Manager (Login):** LightDM 
- **Window Manager:** i3-wm 

## Kickoff: Post-Minimal-Distro Install Steps

### User & Group Setup

We'll start with creating a user and assigning them to the 'wheel' group. As 'casio' is my chosen moniker, we'll go with that (use your username):

```bash
useradd -m -g wheel casio
```

Here, you can set the passwd for your user:

```bash
passwd casio
```

Next, we make sure our new user has sudo powers. We'll edit the sudoers file with Vim:

```bash
vim /etc/sudoers
```

Uncomment this line in the file if you want your user to get sudo powers (but with a passwd prompt everytime it uses them):

```bash
wheel ALL=(ALL) ALL
```

Add this if you don't want to repeat your passwd when running sudo on another terminal:

```bash
Defaults !tty_tickets
```

### Desktop Environment / Window Manager

Let's start by installing Xorg, our graphical environment:

```bash
pacman -S xorg-server xorg-xinit
```

Now, let's get i3, our window manager, up and running. We're also installing a terminal (kitty) and a launcher (dmenu):

```bash
pacman -S i3-wm kitty dmenu
```

You can start the graphical environment with:

```bash
xinit
```

It reads the instructions from ~/.xinitrc on what to kick off. So add "exec i3" into ~/.xinitrc.

### Network Manager

For connecting to the Internet, we're going with nm-applet:

```bash
pacman -S nm-applet
```

### Font Installation

Time to pretty up those terminals:

```bash
pacman -S ttf-linux-libertine
```

### The Panic Button

In case you need mess up everything, remember this life saver:

```bash
Ctrl+Alt+F2/3/4...
```

### Display Managers (Login)

Next up is your display manager LightDM:

```bash
sudo pacman -S lightdm lightdm-gtk-greeter
sudo systemctl enable lightdm.service
```

### Systemd Syntax Basics

Start service at every startup:

```bash
sudo systemctl enable SERVICE_NAME
```

Start service immediately:

```bash
sudo systemctl start SERVICE_NAME
```

### Personalized Startup and Settings

For your user customization, maybe begin setting up your defaults in ~/.profile:

```bash
export PATH=$PATH:$HOME/.scripts
export EDITOR="nvim"
export TERMINAL="kitty"
export BROWSER="brave"
```

If you want to autostart your graphical env on login, add this if-statement:

```bash
if [[ "$(tty)" = "/dev/tty1" ]]; then
    startx
```
