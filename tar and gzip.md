# tar and gzip

## untar ```.tar.xx``` files (where ```xx``` is any extention)

```bash
tar xvf filename.tar.xx
```

### or, to a specific destination folder:

```bash
tar xvf filename.tar.xx -C /some/other/directory
```


## create a tar archive from folder

```bash
tar cvzf filename.tar.gz dirname/
```

## creating a tarball that exculdes some inner folders

```bash
tar --exclude='dir/.git' --exclude='dir/node_modules' -cvzf filename.tar.gz dir/
```

## create a tar and pipe it to stdout instead of a file

```bash
tar -cf - something | base64
```
