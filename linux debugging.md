# Linux debugging commands

* use strace to follow all files opened by a process

```shell
sudo strace -p 1234 -f -s999 -e file
```

* using strace to get a good grasp of what an executable is doing

```shell
strace -f -e file,execve -s9999 <command>
```

* or, to keep the strace output from getting in the way of the program output, use `-o /tmp/filename.strace` to write `strace`'s output to a file

```
strace -f -e file,execve -s9999 -o /tmp/filename.strace <command>
```
