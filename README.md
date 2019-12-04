# raspberrypi-ap

Setup WiFi-AP on **headless** Raspberry Pi.

### Step 1
---

Enable **SSH** on a headless Raspberry Pi (add file to SD card on another machine)

> **SSH** can be enabled by placing a file named ssh, without any extension, onto the boot partition of the SD card from another computer. When the Pi boots, it looks for the ssh file. If it is found, SSH is enabled and the file is deleted.

SSH into raspberrypi
```
ssh pi@raspberrypi
```

### Step 2
---
Upgrade apt-get

```
sudo apt-get update
sudo apt-get upgrade
```

### Step 3
---
Install required softwares

```
sudo apt-get install dnsmasq hostapd
```

### Step 4
---
Turn the new software off and reboot
```
sudo systemctl stop dnsmasq
sudo systemctl stop hostapd
sudo reboot
```

### Step 5
---
Change the SSID and passowrd in the `hostapd.conf` with yours

### Step 6
---
Change the `interface`, DNS IP and the range of dynamic IP with yours in the `dhcpcd.conf` and `hostapd.conf`

### Step 6
---
Put the following configuration files

```
/etc/dhcpcd.conf (DHCP)
/etc/dnsmasq.conf (DNS)
/etc/hostapd/hostapd.conf (HOST AP)
```
Tell the system where to find the hostapd.conf in the /etc/default/hostapd. Find the line with **#DAEMON_CONF**, and replace it with
```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

### Step 7
---
Start the software
```
sudo systemctl start hostapd
sudo systemctl start dnsmasq
sudo reboot
```

### Step 8
---
Check all of the softwares are active (running)

```
service hostapd status
service dnsmasq status
service dhcpcd status
```
