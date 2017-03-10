# Shell/bash scripting

* Comparing variable to string

```bash
if [ "$x" == "string" ]; then
  echo "match"
fi
```

* comparing variable to regex

```bash
if [[ $y =~ reg(ex|ular\ expressions?) ]]; then
  echo "match"
fi
```

NOTE: No use of double quotes, for spaces use `\ `

* Using `while` to perform a command on each line of a file

```bash
while read line; do some-command -on $line; done < file-with-lines
```

NOTE: if any of the commands in the `while` loop is `ssh`, use the `-n` on it to prevent it from forwarding its output to stdin and stop the loop after the first iteration

example:

```bash
while read line; do echo $line:; ssh -n $line "dpkg -l | grep linux-image; uname -a"; done < ~/source_file
```

* for loops

```bash
for var in $(command-that-outputs-delimeted-list); do command-on $f; done
```

* nice trick that combines for and while loops to multithread on a long file

```bash
#start by splitting the file (recommended in its own dir)
split --lines 50 longfile
#create a thread for each of the resulting files (xaa xab xac...)
for f in $(ls|grep ^x); do while read line; do command-on $line; done < $f & done
```
