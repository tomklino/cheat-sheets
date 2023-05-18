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

* Select an object in which a subarry contains a value

```bash
cat something.json | jq 'select(.members[] | contains("username"))'
```

* Use variables from bash within jq
```bash
cat something.json | jq --arg name "$name" '.[] | select(.name==$name)'
```
