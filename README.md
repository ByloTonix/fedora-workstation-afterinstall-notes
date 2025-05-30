<h1 align="center">Fedora Workstation AfterInstall Notes</h1>
<h4 align="center">Things I usually do after installing Fedora Workstation</h4>

![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshots/screenshot0.png)
![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshots/screenshot1.png)
![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshots/screenshot2.png)
![alt text](https://github.com/ByloTonix/fedora-workstation-afterinstall-notes/blob/main/screenshots/screenshot3.png)


## Changing Hostname

```
sudo hostnamectl set-hostname "HOSTNAME"
```

## TPM2.0 Decryption
To decrypt your system without manually entering a password, but using the tpm 2 security module, you can follow this [instruction](https://gist.github.com/jdoss/777e8b52c8d88eb87467935769c98a95)


## System Updating
```
sudo dnf update -y
```

## RPM Fusion
```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf update @core
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
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-plugin-libav --exclude=gstreamer1-plugins-bad-free-devel -y
sudo dnf install lame\* --exclude=lame-devel -y
sudo dnf install gstreamer1-plugin-openh264 mozilla-openh264 -y
sudo dnf group upgrade Multimedia --skip-unavailable
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
sudo visudo /etc/sudoers.d/010_NICKNAME-nopasswd
```
```
NICKNAME ALL=(ALL) NOPASSWD: ALL
```
## Gnome Extensions
* [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)
* [Emoji Copy](https://extensions.gnome.org/extension/6242/emoji-copy/)
* [Rounded Windows Corners Reborn](https://extensions.gnome.org/extension/7048/rounded-window-corners-reborn/)
* [Fullscreen to Empty Workspace](https://github.com/ByloTonix/fullscreen-to-new-workspace-gnome)
* [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
* [Bluetooth Quick Connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
* [App Indicator Support](https://extensions.gnome.org/extension/615/appindicator-support/)
* [Wireless HID](https://extensions.gnome.org/extension/4228/wireless-hid/)
* [Legacy GTK3 Theme Scheme Auto Switcher](https://github.com/mukul29/legacy-theme-auto-switcher-gnome-extension)
* [App Hider](https://extensions.gnome.org/extension/5895/app-hider/)
* [Astra Monitor](https://extensions.gnome.org/extension/6682/astra-monitor/)
* [Grand Theft Focus](https://extensions.gnome.org/extension/5410/grand-theft-focus/)
* [GTK4 Desktop Icons](https://extensions.gnome.org/extension/5263/gtk4-desktop-icons-ng-ding/)
* [Hide Top Bar](https://extensions.gnome.org/extension/545/hide-top-bar/)
* [Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/)
* [Panel Corners](https://extensions.gnome.org/extension/4805/panel-corners/)
* [Quick Settings Tweaker](https://extensions.gnome.org/extension/5446/quick-settings-tweaker/) (with latest fixes from its [GitHub](https://github.com/qwreey/quick-settings-tweaks))
* [RebootToUEFI](https://extensions.gnome.org/extension/5105/reboottouefi/)
* [Media Progress](https://extensions.gnome.org/extension/6940/media-progress/)
  
## Apps
* [BlackBox](https://gitlab.gnome.org/raggesilver/blackbox)
* [Dconf Editor](https://wiki.gnome.org/Apps/DconfEditor)
* [Drawing](https://maoschanz.github.io/drawing/)
* [File Roller](https://wiki.gnome.org/Apps/FileRoller)
* [Geary](https://wiki.gnome.org/Apps/Geary)
* [Gnome Tweaks](https://gitlab.gnome.org/GNOME/gnome-tweaks)
* [Extensions](https://apps.gnome.org/Extensions/)
* [Sound Recorder](https://wiki.gnome.org/Apps/SoundRecorder)
* [VS Code](https://code.visualstudio.com/)
* [Zoom](https://zoom.us/)

## Flatpak Apps
* [Audio Sharing](https://apps.gnome.org/AudioSharing/)
* [Cassette](https://github.com/Rirusha/Cassette)
* [Cohesion](https://github.com/brunofin/cohesion)
* [Gaia Sky](https://zah.uni-heidelberg.de/gaia/outreach/gaiasky/)
* [materialgram](https://github.com/kukuruzka165/materialgram)
* [Metadata Cleaner](https://metadatacleaner.romainvigier.fr)
* [OBS Studio](https://obsproject.com/)
* [Steam](https://store.steampowered.com/)
* [Datcord](https://github.com/gamingdoom/datcord)

## Other
* [Adwaita theme for GTK3](https://github.com/lassekongo83/adw-gtk3)
