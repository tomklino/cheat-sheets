#tar and gzip

## untar ```.tar.xx``` files (where ```xx``` is any extention)

```bash
tar xvf filename.tar.xx
```

## create a tar archive from folder

```bash
tar cvzf filename.tar.gz dirname/
```

## creating a tarball that exculdes some inner folders

```bash
tar --exclude='dir/.git' --exclue='dir/node_modules' -cvzf filename.tar.gz dir/
```
