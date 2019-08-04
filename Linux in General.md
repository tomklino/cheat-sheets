# Linux in General 

- Determining the full path of a command

```bash
which command
```
- Determine what the command is

```bash
type command
```

- Create a user

```
useradd --create-home tomk

# if there are any ssh keys to attach to the user
# paste them in seperate lines in .ssh/authorized_keys (under user home dir)
```

- Determining the package that installed a specific file (Debian)

```bash
dpkg -S /path/to/file
#or, directly on a command like so
dpkg -S `which command`
```

- List files installed by a specific package (Debian)

```bash
dpkg-query -L <package-name>
```

- List files a .deb file will install (Debian)

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
