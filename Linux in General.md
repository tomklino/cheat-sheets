# Linux in General 

- Determining the full path of a command

```bash
which command
```
- Determine what the command is

```bash
type command
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

1. `--x`
2. `-w-`
3. `-wx`
4. `r--`
5. `r-x`
6. `rw-`
7. `rwx`

- Show all the sudo permissions of a user

```bash
sudo -l
```

- Using less with color:

```bash
jq -C . data.json | less -R
```
