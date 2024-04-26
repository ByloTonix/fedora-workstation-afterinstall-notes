<h1 align="center">Fedora Workstation AfterInstall Notes</h1>
<h4 align="center">Things I do after installing Fedora Workstation</h4>

![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshot0.png)

## Enabling Root User && Changing Hostname

```
sudo passwd root
```
```
sudo hostnamectl set-hostname "hp"
```

## DNF Config for a slightly faster download
```
sudo nano /etc/dnf/dnf.conf
``` 
```
[main]
gpgcheck=True
installonly_limit=3
clean_requirements_on_remove=True
best=False
skip_if_unavailable=True
max_parallel_downloads=10
``` 
## System Updating
```
dnf check-update
```

## RPM Fusion
```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf groupupdate core
```

## Firmware
```
sudo fwupdmgr get-devices 
sudo fwupdmgr refresh --force 
sudo fwupdmgr get-updates 
sudo fwupdmgr update
```

## Additional Codecs
```
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-plugin-libav --exclude=gstreamer1-plugins-bad-free-devel
sudo dnf install lame\* --exclude=lame-devel
sudo dnf install gstreamer1-plugin-openh264 mozilla-openh264
sudo dnf group upgrade --with-optional Multimedia
```

## Decreasing TouchPad Scroll Speed
```
sudo dnf install libinput-devel
git clone https://gitlab.com/warningnonpotablewater/libinput-config
sudo dnf install make cmake automake gcc gcc-c++ kernel-devel meson
sudo dnf install rust-libudev-devel --setop='install_weak_deps=False'
cd libinput-config/ && meson build
cd build/ && ninja
sudo ninja install
sudo dnf remove rust-libudev-devel
sudo nano /etc/libinput.conf
```
```
scroll-factor=0.25
```

## No Password
```
sudo visudo /etc/sudoers.d/010_revoqaux-nopasswd
```
```
revoqaux ALL=(ALL) NOPASSWD: ALL
```
## Gnome Extensions
* [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)
* [Emoji Copy](https://github.com/felipeftn/emoji-copy)
* [Rounded Windows Corners](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/rounded-window-corners.zip)
* [Fullscreen to Empty Workspace](https://github.com/ByloTonix/fullscreen-to-new-workspace-gnome-46)
* [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
* [Bluetooth Quick Connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
* [App Indicator Support](https://extensions.gnome.org/extension/615/appindicator-support/)
* [Wireless HID](https://extensions.gnome.org/extension/4228/wireless-hid/)
* [Legacy GTK3 Theme Scheme Auto Switcher](https://github.com/mukul29/legacy-theme-auto-switcher-gnome-extension)

## Other
* [Adwaita theme for GTK3](https://github.com/lassekongo83/adw-gtk3)
