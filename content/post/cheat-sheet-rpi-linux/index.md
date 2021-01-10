+++
author = "jfdzar"
title = "Cheat Sheet RaspberryPi Linux"
date = "2020-02-25"
description = "Interesting Linux Commands for Raspberry Pi"
tags = [
    "linux",
    "raspberry",
    "cheatsheet"
]
categories = [
    "sys-admin"
]
+++

In this entry I would document some interesting linux commands to use in the raspberry pi

* To see the history of commands you typed
{{< highlight bash >}}
history
{{< /highlight >}}

* Different for sudo and user
{{< highlight bash >}}
crontab -e
{{< /highlight >}}

* To connect to the raspberry pi remotely from other laptop through ssh
{{< highlight bash >}}
ssh user@ipofthehost
{{< /highlight >}}

* Correr el script y guardar el output en output.log
{{< highlight bash >}}
nohup python /path/to/test.py > output.log &
{{< /highlight >}}

* Ver que PID tiene el script de python
{{< highlight bash >}}
ps ax | grep test.py
{{< /highlight >}}

* Matar el proceso (PID = el numero)
{{< highlight bash >}}
kill PID
{{< /highlight >}}

* list of devices
{{< highlight bash >}}
dmesg
{{< /highlight >}}

* list of USB devices
{{< highlight bash >}}
lsusb
{{< /highlight >}}

* kernel of linux used
{{< highlight bash >}}
uname -r
{{< /highlight >}}

* look for "8192" in /
{{< highlight bash >}}
find / -name "8192" -print
{{< /highlight >}}

* check loaded modules
{{< highlight bash >}}
lsmod
{{< /highlight >}}

* mount network device need cifs-utils needs root
{{< highlight bash >}}
mount -t cifs -o username=juan //server /localfolder
{{< /highlight >}}

* change samba password of osmc user
{{< highlight bash >}}
smbpasswd -a osmc
{{< /highlight >}}

* delete folder and its content
{{< highlight bash >}}
rm -r foldername
{{< /highlight >}}

* Download file from ssh server
{{< highlight bash >}}
scp pi@pisalamanca:/home/pi/ovpns/jfdzar_mobile.ovpn jfdzar_mobile.ovpn
{{< /highlight >}}