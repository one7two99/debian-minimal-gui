# Minimal Debian with a GUI
Debian 12.5 + Wayland + Sway

- Install Debian minimal without any additional packages
- Create a /boot and a partition fur LUKS encryption
- Use the LUKS partition as physicall volume for LVM
- Create a volume group and three logical volumes for / and /home and /swap

## Get a network connection
To install further packages I used my mobile via USB tethering
```
dhclient 
ip a
```

## Install Core Tools
```
apt-get install man git mc nano mlocate sudo network-manager wlr-randr htop
usermod -aG sudo user
logout
wlr-randr --output eDP-1 --off
updatedb
echo "PATH=$PATH:/usr/sbin" >> /etc/bash.bashrc 
```

## Install sway
```
apt-get install sway
export "XDG_RUNTIME_DIR=/run/user/$(id -u)" >> ~/.bashrc
mkdir -p ~/.config/sway
cp /etc/sway/config ~/.config/sway
nano ~/.config/sway/config
cp /etc/xdg/foot/foot.ini .config/foot
```

## Install greetd
```
apt-get install greetd
nano /etc/greetd/config.toml 
# change line to:
command = "/usr/sbin/agreety --cmd sway"
```

## Further sway setup
```
apt-get install swaybar pulseaudio fonts-font-awesome pavucontrol grimshot swayimg wofi
# suggested: jackd2 pipewire sndiod libappindicator3-1

# Change .config/sway/config:
# set $menu dmenu_path | dmenu | xargs swaymsg exec --
set $menu wofi --show run    

# Setup waybar
download waybar default config to
mkdir -p ~/.config/waybar
# See also https://linuxconfig.org/how-to-install-configure-and-customize-waybar-on-linux
```
## Install additional programs
apt-get install qutebrowser firefox
