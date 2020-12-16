# jq

* List paths of all the json file

```bash
cat something.json | jq -c 'path(..)|[.[]|tostring]|join("/")'
```

* Filter array based on an argument in the object

```bash
cat something.json | jq '.[] | select(.name=="Tom")'
```

* Filter array based on an argument matching a regex

```bash
cat something.json | jq '.[] | select(.city|test("[Rr]amat"))'
```

* Use variables from bash within jq
```bash
cat something.json | jq --arg name "$name" '.[] | select(.name==$name)'
```
