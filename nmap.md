# nmap

## good to know

### adding `-oG -` to the end of the command make easier to parse

## common usage

### ping scan a range

```bash
nmap -sP 10.0.0.1-254
```

### scan a few specific ports on a range of IPs

```bash
nmap -p22,80,443 192.168.0.0/24
```

### scan a range of ports

```bash
nmap -p1024-5060 192.168.0.1
```
