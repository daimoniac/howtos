# [RaspPi] Virtual Accesspoint on Xbian
Little How To to get an Virtual AP running on XBian.

## Install software
```
cd /etc/rcS.d
ln -s ../init.d/udev S01udev
apt-get update
apt-get install install hostapd hostap-utils iw bridge-utils
```

## Configure hostapd
sudo vi /etc/hostapd/hostapd.conf

```
interface=wlan0
bridge=br0
ssid=my_essid
hw_mode=g
ieee80211n=1
channel=11
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=Password
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

sudo vi /etc/default/hostapd

```
DAEMON_CONF="/etc/hostapd/hostapd.conf
```

## Configure hostapd autostart
```
sudo update-rc.d hostapd enable
```

## Configure IPv4 Forward
sudo vi /etc/sysctl.conf

```
net.ipv4.ip_forward=1
```

## Configure interfaces

sudo vi /etc/network/interfaces

```
auto lo br0
iface lo inet loopback

iface eth0 inet dhcp

allow hotplug wlan0
iface wlan0 inet manual

iface br0 inet static
bridge-ports eth0 
address 192.168.142.108
netmask 255.255.255.0
network 192.168.142.0
broadcast 192.168.142.255
gateway 192.168.142.1
```

## Configure rc.local for boot
sudo vi /etc/rc.local  

add before exit 0  

```
ifup br0
```

8.) Reboot
sudo reboot


based upon
https://www.nico-maas.de/?p=962
