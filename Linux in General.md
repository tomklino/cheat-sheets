# Linux in General 

- Determining the full path of a command

```bash
which command
```

- Determining the package that installed a specific file

```bash
dpkg -S /path/to/file
#or, directly on a command like so
dpkg -S `which command`
```
