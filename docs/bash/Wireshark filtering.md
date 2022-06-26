
## Filter

```
ip.addr == 192.168.0.1 && http
```

## Tcp

```
tcpdump -i enp0s8 -s 0 -A 'tcp dst port 80 and tcp\[((tcp\[12:1\] & 0xf0) >> 2):4\] = 0x504F5354'
```