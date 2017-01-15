# tshark and tcpdump

## tshark

* capture on all interfaces

```bash
tshark -ni any
```

* dump to pcap file (any packet that passed the capture filter, or all if there isn't any)

```bash
tshark -w outfie.pcap
```

### filters

* for display filters

```bash
tshark -Y <display filter>
```
 
 * for capture filter
 
 ```bash
 tshark -f <capture filter>
 ```
 
 * filter by destination tcp port
 
 ** display filter ```tcp.dstport==80```
 
 ** capture filter ```tcp dst port 80```
