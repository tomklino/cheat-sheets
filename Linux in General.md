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

- List files installed by a specific package

```bash
dpkg-query -L <package-name>
```

- List files a .deb file will install

```bash
dpkg-deb -c <package-name.deb>
```

- `chmod` numbers representation:

1. `--x` execute
2. `-w-` write
3. `-wx`
4. `r--` read
5. `r-x`
6. `rw-`
7. `rwx`
