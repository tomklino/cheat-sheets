# Linux debugging commands

### use strace to follow all files opened by a process

```shell
sudo strace -f ohai 2>&1 >/dev/null | grep ^open\( | grep -v ENOENT | sed 's/^.*\"\(.*\)".*$/\1/' | sort | uniq | tee ~/opened_by_ohai
```

### another way to track all files opened by a process

```shell
sudo strace -p 1234 -f -s999 -e trace=open -e trace=openat
```
