# some comments on a few things

# bootloader: grub
# init system: systemd (check init.d)
# display renderer: xorg (check wayland)
# display manager (login): lightdm (check gdm [gnome dm])
# desktop env?: i3 [check dwm]


# artix instead of arch?
why? no systemd (bloat?). Like an arch equivalent but with no systemd, kind of easier to get it working. Openrc instead of systemd...
Na, I'll use arch for now. 

# after installing minimal distro

+ users and groups
useradd -m -g wheel casio
passwd casio
vim /etc/sudoers
-> uncomment: wheel ALL=(ALL) ALL
Defaults !tty_tickets

+ DE / WM -> wm

firstly install xorg (a graphical env)
pacman -S xorg-server xorg-xinit

$ xinit 
    - (starts graphical env)
    - reads from ~/.xinitrc what to start
    - add "exec i3" into ~/.xinitrc
    - $ startx 

install i3
pacman -S i3-wm kitty dmenu
(installing wm, terminal and launcher respect)

installing a network manager (nm-applet)
pacman -S nm-applet

install some fonts
pacman -S ttf-linux-libertine

ok maybe i have to check out dwm

# tip: if i mess up something -> ctrl+alt+f2/3/4...

+ display managers (login)
lightdm
sudo pacman -S lightdm lightdm-gtk-greeter
sudo systemctl enable lightdm.service


# some systemd syntax 
start service every startup:
$ sudo systemctl enable SERVICE_NAME

start service just now:
$ sudo systemctl start SERVICE_NAME

# customizing user startup and settings
~/.profile -> 
export PATH=$PATH:$HOME/.scripts
export EDITOR="nvim"
export terminal="kitty"
export BROWSER="brave"

if [[ "$(tty)" = "/dev/tty1" ]]; then
    pgrep i3 || startx

~/.bash_profile
~/.zshrc


packages:
    + intel graph drivers: xf86-video-intel
    + 




## Considering Artix?

Artix Linux: it's the Arch without Systemd, supposedly a leaner, meaner version. Some people claim it's easier to get running, swapping out Systemd for OpenRC. But for this round, we're sticking to Arch.
