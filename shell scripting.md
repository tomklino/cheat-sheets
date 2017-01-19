# Shell/bash scripting

* Comparing variable to string

```
if [ "$x" == "string" ]; then
  echo "match"
fi
```

* Using while to perform a command on each line of a file

```bash
while read line; do some-command -on $line; done < file-with-lines
```
