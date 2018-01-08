# sed

## gereral notes

* add ```-i file_name``` to edit a file and save the changes and don't do that when piping into sed to edit a stream
* don't forget to add ```g``` in the end of the sed expression if there is more than a single substitution per line

## sed tricks

* remove the first 3 lines from file:

```bash
sed '1,3d'
```

* remove leading whitespaces from file:

```bash
sed 's/^[ \t]*//'
```

* shorten all the words in a line to 3 letters:

```bash
sed -r 's/([a-z]{3})[a-z]*/\1/g'
```

* comment out the entire file (with `#`):

```bash
sed 's/^\(.*\)/#\1/'
```

* uncomment all comments from a file:

```bash
sed 's/^#*//'
```

* remove blank lines from output

```bash
sed '/^ *$/d'
```

* remove new line (pull next line up) in case line has a specific regex
(see https://stackoverflow.com/questions/25944087/ for details)

```bash
sed '/regex/{N;s/\n//;}'
```

* adding text to the end of a line

```bash
#add hello to the end of all lines in a file
sed 's/$/hello/'
#add hi to the end of each line matching a regex
sed '/h+[123]/s/$/hi/'
```

# awk

* print only lines shorter than 80 notes

```bash
awk "{if (length(\$0) < 80){print \$0}}"
```

* use awk to match only the command part of history list

```bash
history | awk 'match($2, /^ssh$/) {print $0}'
```

or

```bash
history | awk '$2~/^ssh$/ {print $0}'
```

* use awk with variables from shell

```bash
awk -v var=$var '$1 == var {print $2}';
```

* change the default delimeter of awk

```bash
#read csv files
awk -F',' '$1 == "something" {print $0}';
```

* start printing only after a specific regex was found

```bash
awk 'BEGIN{f=0}; /regex/{f=1} {if(f) print}'
```

* print from line x to line y:

```bash
awk 'BEGIN{f=0}; NR == 118 {f=1} {if(f) print} NR == 128 {f=0}' < /path/to/file
```

* print column x of line y:

```bash
# print column 1 of line 4
awk 'FNR==4 {print $1}'
```
