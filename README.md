<h1 align="center">Fedora Workstation AfterInstall Notes</h1>
<h4 align="center">Things I do after installing Fedora Workstation</h4>

![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshot0.png)

## Enabling Root User && Changing Hostname

```
sudo passwd root
```
```
sudo hostnamectl set-hostname "asus"
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
sudo dnf -y update
sudo dnf -y upgrade --refresh
```

## RPM Fusion
```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```
```
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
sudo dnf group upgrade --with-optional Multimedia
```
## Hardware Acceleration (AMD) 
```
sudo dnf install ffmpeg ffmpeg-libs libva libva-utils
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
```
```
sudo dnf config-manager --set-enabled fedora-cisco-openh264
sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264
```

## Laptop Sleep Mode Fix
```
sudo grubby --update-kernel=ALL --args="mem_sleep_default=s2idle"
```

## Disable Gnome Software Autostart
```
sudo rm /etc/xdg/autostart/org.gnome.Software.desktop
```

## Decreasing TouchPad Scroll Speed
```
sudo dnf install libinput-devel
git clone https://gitlab.com/warningnonpotablewater/libinput-config
sudo dnf install make cmake automake gcc gcc-c++ kernel-devel
sudo dnf install rust-libudev-devel-0.3.0-3.fc39.noarch --setop='install_weak_deps=False'
cd libinput-config/ && meson build
cd build/ && ninja
sudo ninja install
sudo dnf remove rust-libudev-devel-0.3.0-3.fc39.noarch
sudo nano /etc/libinput.conf
```
```
scroll-factor=0.25
```


## Additional Changes
```
sudo dnf remove gnome-boxes gnome-logs gnome-font-viewer gnome-remote-desktop orca abrt python2
gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true
systemctl disable gnome-software-service-proxy
systemctl disable evolution-data-server
systemctl --user mask org.gnome.SettingsDaemon.Wacom
systemctl --user mask org.gnome.SettingsDaemon.PrintNotifications
systemctl --user mask org.gnome.SettingsDaemon.A11ySettings
systemctl --user mask org.gnome.SettingsDaemon.Smartcard
systemctl --user mask org.gnome.SettingsDaemon.Housekeeping
systemctl --user mask evolution-addressbook-factory.service evolution-calendar-factory.service evolution-source-registry.service
systemctl --user mask org.gnome.SettingsDaemon.Sharing
```
## No Password
```
sudo visudo /etc/sudoers.d/010_YOURNICKNAME-nopasswd
```
```
bylotonix ALL=(ALL) NOPASSWD: ALL
```
## Gnome Extensions
* [Compiz Windows Effect](https://extensions.gnome.org/extension/3210/compiz-windows-effect/)
* [Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/)
* [Rounded Windows Corners](https://extensions.gnome.org/extension/5237/rounded-window-corners/) from comments
* [Fullscreen to Empty Workspace](https://extensions.gnome.org/extension/6072/fullscreen-to-empty-workspace/)
* [Windows Is Ready Notification Remover](https://extensions.gnome.org/extension/1007/window-is-ready-notification-remover/)
* [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
* [Quick Settings Tweaker](https://extensions.gnome.org/extension/5446/quick-settings-tweaker/)
* [Bluetooth Quick Connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
* [App Indicator Support](https://extensions.gnome.org/extension/615/appindicator-support/)
* [Wireless HID](https://extensions.gnome.org/extension/4228/wireless-hid/)

* [Battery Time](https://extensions.gnome.org/extension/1475/battery-time/)
* [Burn My Windows](https://extensions.gnome.org/extension/4679/burn-my-windows/)
* [Compact Top Bar](https://extensions.gnome.org/extension/5669/compact-top-bar/)
* [Compiz alike magic lamp effect](https://extensions.gnome.org/extension/3740/compiz-alike-magic-lamp-effect/)
* [Desktop Cube](https://extensions.gnome.org/extension/4648/desktop-cube/)
* [Removable Drive Menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
* [Notification Banner Position](https://extensions.gnome.org/extension/4105/notification-banner-position/)
* [Flippery Move Clock](https://extensions.gnome.org/extension/2/move-clock/)

## Apps
```
sudo dnf install unzip p7zip p7zip-plugins unrar
sudo dnf install kolourpaint obs-studio blender htop audacity audacious vlc file-roller
sudo dnf install neofetch --setop='install_weak_deps=False'
sudo dnf install xwaylandvideobridge
sudo dnf install waydroid
```
[VSCode](https://code.visualstudio.com/sha/download?build=stable&os=linux-rpm-x64)
## Firefox Gnome Theme:
```
curl -s -o- https://raw.githubusercontent.com/rafaelmardojai/firefox-gnome-theme/master/scripts/install-by-curl.sh | bash
```
