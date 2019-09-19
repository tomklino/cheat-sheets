# networking
## Setting up a new NIC:


* in RH/CentOS:

```bash
		cd /etc/sysconfig/network-scripts
		cat >> ifcfg-eth1
			DEVICE=eth1
			HWADDR=08:00:27:72:1D:FC
			TYPE=Ethernet
			ONBOOT=yes
			NM_CONTROLLED=yes
			BOOTPROTO=dhcp
```
* OR for static IP:
	
```bash
		cat >> /etc/sysconfig/network
			NETWORKING=yes
			HOSTNAME=server1.cyberciti.biz
			GATEWAY=192.168.1.254
```

AND:

```bash
		cat > /etc/sysconfig/network-script/ifcfg-eth1
			DEVICE=eth1
			HWADDR=08:00:27:72:1D:FC
			IPADDR=192.168.1.10
			NETMASK=255.255.255.0
			TYPE=Ethernet
			ONBOOT=yes
			NM_CONTROLLED=yes
			BOOTPROTO=static
```
* in Debain:

```bash
		cd /etc/network
		cat >> interfaces
			allow-hotplug eth1
			iface eth1 inet dhcp
```
* OR for static IP:

```bash
		cat >> interfaces:
			iface eth0 inet static
  			    address 192.168.1.10
 			    network 192.168.1.0
   			    netmask 255.255.255.0
   			    broadcast 192.168.1.255
  			    gateway 192.168.1.254
```
## flushing dns
```bash
service dnsmasq restart
```

## manipulating routes

* adding route
```bash
route add -net 10.10.10.0/24 gw 192.168.0.1
```

or

```bash
route add -host 10.10.10.45 gw 192.168.0.1
```

* deleting route
```bash
route del -net 10.10.10.0/24 gw 192.168.0.1
```

or

```bash
route del -host 10.10.10.45 gw 192.168.0.1
```

* Turning ip forwarding on or off

```bash
sysctl -w net.ipv4.ip_forward=0 # off
sysctl -w net.ipv4.ip_forward=1 # on
sysctl net.ipv4.ip_forward # check value with no change
```

## iptables

* add a rule to allow from ip

```bash
iptables -A INPUT -s 192.168.1.1 -j ACCEPT
```

* delete a rule by its number

first, display the rule numbers as such

```bash
iptables -nvL --line-numbers
```

remove the first rule of the INPUT chain

```bash
iptables -D INPUT 1
```

## tracking traffic on a specific interface and port
```bash
tcpdump -i eth0 'port 80'
```

* neat trick to track captured traffic on remote server directly in wireshark
```bash
#IMPORTANT: a capture filter is necessary so not to track ssh packets of the connection itself and creating an infinite loop
ssh full.fqdn.com sudo tcpdump -s0 -n -w - <capture-filter> | wireshark -k -i -
```
