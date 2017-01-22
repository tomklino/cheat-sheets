# Shell/bash scripting

* Comparing variable to string

```
if [ "$x" == "string" ]; then
  echo "match"
fi
```

* Using `while` to perform a command on each line of a file

```bash
while read line; do some-command -on $line; done < file-with-lines
```

NOTE: if any of the commands in the `while` loop is `ssh`, use the `-n` on it to prevent it from forwarding its output to stdin and stop the loop after the first iteration

example:

```bash
while read line; do echo $line:; ssh -n $line "dpkg -l | grep linux-image; uname -a"; done < ~/source_file
```
