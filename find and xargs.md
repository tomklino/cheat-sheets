# find and xargs

* common ways to look for files

```bash
find -name "exact name"
find -name "*with wildcards*"
find -regex "reg(ex|ular expressions)"
```

* limiting the depth

```bash
#checks only working directory
find -name "filename" -maxdepth 1
```

* based on file date metadata

```bash
#find files newer than otherfile
find -newer otherfile

#find files older than 5 days
find -mtime +5

#find and delete files older than 5 days in current directory
find . -maxdepth 1 -mtime +5 -exec rm {} \;
```

* based on the size of the file

```bash
#find files bigger than 500M
find -type f -size +500M
```
