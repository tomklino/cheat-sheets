# sed

## gereral notes

* add ```-i file_name``` to edit a file and save the changes and don't do that when piping into sed to edit a stream
* don't forget to add ```g``` in the end of the sed expression if there is more than a single substitution per line

remove leading whitespaces from file:

```sed 's/^[ \t]*//'```

shorten the first word in a line to 3 letters:

```sed -r 's/([a-z]{3})[a-z]*/\1/'```

# awk

print only lines shorter than 80 notes

awk "{if (length(\$0) < 80){print \$0}}"
