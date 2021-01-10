+++
author = "jfdzar"
title = "WiFi Access Point with Raspberry Pi"
date = "2020-02-25"
description = "Create a WiFi Access Point with a Raspberry Pi"
tags = [
    "linux",
    "raspberry",
    "homeassistant"
]
categories = [
    "sys-admin",
    "home-assistant"
]
+++

[Source: The Pi](https://thepi.io/how-to-use-your-raspberry-pi-as-a-wireless-access-point/)


* First install hostapd and dnsmasq
{{< highlight bash >}}
sudo apt-get install hostapd
sudo apt-get install dnsmasq
{{< /highlight >}}

* Stop both services
{{< highlight bash >}}
sudo systemctl stop hostapd
sudo systemctl stop dnsmasq
{{< /highlight >}}

* Configure Statis IP for Wlan0 interface
{{< highlight bash >}}
sudo nano /etc/dhcpcd.conf
{{< /highlight >}}

* Write the following at the end of the file
{{< highlight bash >}}
interface wlan0
static ip_address=192.168.0.10/24
denyinterfaces eth0
denyinterfaces wlan0
{{< /highlight >}}

* Configure DHCP Server
{{< highlight bash >}}
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf
{{< /highlight >}}

* Write the following in the file
{{< highlight bash >}}
interface=wlan0
  dhcp-range=192.168.0.11,192.168.0.30,255.255.255.0,24h
{{< /highlight >}}

* Configure the access point host software (hostapd)
{{< highlight bash >}}
sudo nano /etc/hostapd/hostapd.conf
{{< /highlight >}}

* Write the following in the file
{{< highlight bash >}}
interface=wlan0
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
ssid=NETWORK
wpa_passphrase=PASSWORD
{{< /highlight >}}

* Show the system the location of the file
{{< highlight bash >}}
sudo nano /etc/default/hostapd
{{< /highlight >}}

* Write the following to the file
{{< highlight bash >}}
DAEMON_CONF="/etc/hostapd/hostapd.conf"
{{< /highlight >}}

*I had problems starting the services hostapd and I follow the instructions of this [link](https://www.raspberrypi.org/forums/viewtopic.php?t=237684) running the following commands it worked…

I also run something of the ip_tables but I do not know if it was related. Edited: No it was not related the ip_tables are only used to redirect the traffic from the port with internet to the wifi access point

{{< highlight bash >}}
sudo systemctl unmask hostapd
sudo systemctl enable hostapd
sudo systemctl start hostapd
{{< /highlight >}}