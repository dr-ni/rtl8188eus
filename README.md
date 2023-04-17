## rtl8188eus v5.3.9

# Realtek rtl8188eus &amp; rtl8188eu &amp; rtl8188etv WiFi drivers

# Howto build/install
1. You will need to blacklist another driver in order to use this one.
2. `echo 'blacklist r8188eu'|sudo tee -a '/etc/modprobe.d/realtek.conf'`
3. Reboot
4. cd rtl8188eus
5. `make && sudo make install`
6. Reboot in order to blacklist and load the new driver/module.

# MONITOR MODE howto
Use these steps to enter monitor mode.
```
$ sudo airmon-ng check kill
$ sudo ip link set <interface> down
$ sudo iw dev <interface> set type monitor
```
Frame injection test may be performed with
(after kernel v5.2 scanning is slow, run a scan or simply an airodump-ng first!)
```
$ aireplay -9 <interface>
```

## How to install (for arm devices)

`sudo ln -s /lib/modules/$(uname -r)/build/arch/arm /lib/modules/$(uname -r)/build/arch/armv7l`

`sudo apt-get install build-essential git dkms linux-headers-$(uname -r)`

`git clone -b arm https://github.com/kelebek333/rtl8188fu rtl8188fu-arm`

`sudo dkms add ./rtl8188fu-arm`

`sudo dkms build rtl8188fu/1.0`

`sudo dkms install rtl8188fu/1.0`

`sudo cp ./rtl8188fu-arm/firmware/rtl8188fufw.bin /lib/firmware/rtlwifi/`

------------------

# NetworkManager configuration
Add these lines below to "NetworkManager.conf" and ADD YOUR ADAPTER MAC below [keyfile]
This will make the Network-Manager ignore the device, and therefore don't cause problems.
```
[device]
wifi.scan-rand-mac-address=no

[ifupdown]
managed=false

[connection]
wifi.powersave=0

[main]
plugins=keyfile

[keyfile]
unmanaged-devices=mac:A7:A7:A7:A7:A7
```

# Credits
Realtek       - https://www.realtek.com<br>
Alfa Networks - https://www.alfa.com.tw<br>
aircrack-ng.  - https://www.aircrack-ng.org<br>
<br>
And all those who may be using or contributing to it of anykind. Thanks!<br>
