# sed

## gereral notes

* add ```-i file_name``` to edit a file and save the changes and don't do that when piping into sed to edit a stream
* don't forget to add ```g``` in the end of the sed expression if there is more than a single substitution per line

## sed tricks

### remove leading whitespaces from file:

```bash
sed 's/^[ \t]*//'
```

### shorten all the words in a line to 3 letters:

```bash
sed -r 's/([a-z]{3})[a-z]*/\1/g'
```

### comment out the entire file (with `#`):

```bash
sed 's/^\(.*\)/#\1/'
```

### uncomment all comments from a file:

```bash
sed 's/^#*//'
```

# awk

### print only lines shorter than 80 notes

```bash
awk "{if (length(\$0) < 80){print \$0}}"
```

### use awk to match only the command part of history list

```bash
history | awk 'match($2, /^ssh$/) {print $0}'
```
