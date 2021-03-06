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

* excluding a dir from the search

```bash
find . -name "file-5" -not -path "./oh/*" -not -path "./no/*"
```

* searching files by their checksum

```bash
find ~ -type f -exec md5sum {} \;| grep 1797eaf5aeb776cffbbc93c5376ec7ab
# it is recomended to limit the file size as checksum on large files is cpu intensive
find ~ -type f -size -10M -exec md5sum {} \;| grep 1797eaf5aeb776cffbbc93c5376ec7ab
```

* search for files by a regex they contain and limiting the search to small files only
```bash
find ~ -type f -size -10k -exec grep -EH reg(ex|ular\ expression) \;
```
