 # Fedora Workstation AfterInstall Notes
Things I do after installing Fedora Workstation

## Root User
``sudo passwd root``

## Changing Hostname
``sudo hostnamectl set-hostname "asus"``

## DNF Config
`sudo nano /etc/dnf/dnf.conf` 
```
[main]
gpgcheck=True
installonly_limit=3
clean_requirements_on_remove=True
best=False
skip_if_unavailable=True
max_parallel_downloads=10
``` 
## Update 
``sudo dnf -y update
sudo dnf -y upgrade --refresh``

## RPM Fusion
``sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm``
``sudo dnf groupupdate core``

## Firmware
```
sudo fwupdmgr get-devices 
sudo fwupdmgr refresh --force 
sudo fwupdmgr get-updates 
sudo fwupdmgr update
```

## Codecs
````
sudo dnf groupupdate 'core' 'multimedia' 'sound-and-video' --setop='install_weak_deps=False' --exclude='PackageKit-gstreamer-plugin' --allowerasing && sync
sudo dnf swap 'ffmpeg-free' 'ffmpeg' --allowerasing
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel ffmpeg gstreamer-ffmpeg
sudo dnf install lame\* --exclude=lame-devel
sudo dnf group upgrade --with-optional Multimedia
````

## Hardware Acceleration (AMD) 
`sudo dnf install ffmpeg ffmpeg-libs libva libva-utils`
```
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
```
`sudo dnf config-manager --set-enabled fedora-cisco-openh264`
`sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264`

## Laptop Sleep Mode Fix
`sudo grubby --update-kernel=ALL --args="mem_sleep_default=s2idle"`

## Disable Gnome Software Autostart
`sudo rm /etc/xdg/autostart/org.gnome.Software.desktop`

## Decreasing TouchPad Scroll Speed
```sudo dnf install libinput-devel
git clone https://gitlab.com/warningnonpotablewater/libinput-config
sudo dnf install make cmake automake gcc gcc-c++ kernel-devel
sudo dnf install rust-libudev-devel-0.3.0-3.fc39.noarch --setop='install_weak_deps=False'
cd libinput-config/ && meson build
cd build/ && ninja
sudo ninja install
sudo dnf remove rust-libudev-devel-0.3.0-3.fc39.noarch
sudo nano /etc/libinput.conf
```
`scroll-factor=0.25`

## XWayland Video Bridge
``sudo dnf install xwaylandvideobridge``


### Additional changes:
```sudo dnf install neofetch --setop='install_weak_deps=False'
sudo dnf remove orca
gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true
sudo dnf remove abrt
sudo dnf remove python2
systemctl disable gnome-software-service-proxy
systemctl disable evolution-data-server
systemctl list
systemctl --user mask org.gnome.SettingsDaemon.Wacom
systemctl --user mask org.gnome.SettingsDaemon.PrintNotifications.
systemctl --user mask org.gnome.SettingsDaemon.A11ySettings
systemctl --user mask org.gnome.SettingsDaemon.Smartcard
systemctl --user mask org.gnome.SettingsDaemon.Housekeeping.service 
systemctl --user mask evolution-addressbook-factory.service evolution-calendar-factory.service evolution-source-registry.service
systemctl --user mask org.gnome.SettingsDaemon.Sharing.service

sudo dnf remove gnome-boxes-45.0-1.fc39.x86_64 gnome-logs-45~beta-1.fc39.x86_64 gnome-font-viewer-45.0-1.fc39.x86_64 gnome-remote-desktop-45.1-1.fc39.x86_64
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

## Apps
 `sudo dnf install -y unzip p7zip p7zip-plugins unrar`
* Firefox Gnome Theme:
```curl -s -o- https://raw.githubusercontent.com/rafaelmardojai/firefox-gnome-theme/master/scripts/install-by-curl.sh | bash```
