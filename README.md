# VR-in-Linux-Ubuntu-manual
How to run VR projects (Unity) in Ubuntu

WIKI: https://github.com/CyberKoalaStudios/VR-in-Linux-Ubuntu-manual/wiki

First things first:
## 1. Dependencies

```bash
$ sudo apt-get install libusb-dev libudev-dev libxinerama-dev libxrandr-dev
$ sudo apt-get install adb
```

## 2. Add user to usergroup to connect HMD
Run all commands with sudo (important). Change `${YOUR_USER_NAME}` to your linux account name (admin)
```bash
$ sudo useradd -aG plugdev ${YOUR_USER_NAME}
```

## 3. Create ADB Rules file
```bash
$ sudo nano /etc/udev/rules.d/50-oculus.rules
```
### Only for oculus (but you can find ATTR for other HMD too):
```bash
## 5etc/udev/rules.d/50-oculus.rules
SUBSYSTEM="usb", ATTR{idVendor}=="2833", ATTR{idProduct}=="0186", MODE="0660" group="plugdev", symlink+="ocuquest%n" 
```

```bash
$ sudo udevadm control --reload-rules
```

## 4. Restart PC (important!) reboot

## 5. Restart ADB
```bash
$ sudo adb kill-server  
$ sudo adb start-server  
```

## 6. Connect your HMD via USB 3.0 cable and run:
```
$ sudo adb devices  
```

Successfull output should be like this:
```bash
List of devices attached
1WWWAAAFFFF device
```

---

## HOWTO install VR software

Optional: install Steam VR via deb package https://store.steampowered.com/about/
or terminal:
```bash
$ sudo apt update
$ sudo apt install steam
```

Optional: install SideQuest https://github.com/SideQuestVR/SideQuest/releases
It can link your HMD via WIFI - very helpful feature
```bash
$ wget https://github.com/SideQuestVR/SideQuest/releases/download/v0.10.33/SideQuest-0.10.33.tar.xz
$ tar -xvf SideQuest-0.10.33.tar.xz
$ cd SideQuest-0.10.33
$ ./sidequest
```

Unity HUB: https://docs.unity3d.com/hub/manual/InstallHub.html?_ga=2.186802408.1785355613.1677948539-252450891.1661446378#install-hub-linux


Useful links:
* Monado (OpenXR free open-source alternative): https://gitlab.freedesktop.org/monado/monado
* ALVR: https://github.com/alvr-org/alvr
