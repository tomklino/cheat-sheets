# jq

* List paths of all the json file

```bash
jq -r 'path(..)|[.[]|tostring]|join("/")'
```

* Filter array based on an argument in the object

```bash
jq '.[] | select(.name=="Tom")'
```

* Filter array based on an argument matching a regex

```bash
jq '.[] | select(.city|test("[Rr]amat"))'
```

* Select an object in which a subarry contains a value

```bash
jq 'select(.members[] | contains("username"))'
```

* Use variables from bash within jq

```bash
jq --arg name "$name" '.[] | select(.name==$name)'
```
* Translate a unix time to ISO format:

```bash
# input { timestamp: 1683190330 } (timestamp in seconds)
jq '.timestamp | strftime("%Y-%m-%dT%H:%M:%SZ")'

# input { timestamp: 1683190330454 } (timestamp in milliseconds)
jq '.timestamp | ./1000 | strftime("%Y-%m-%dT%H:%M:%SZ")'

# input { timestamp: "1683190330454" } (timestamp is string in milliseconds)
jq '.timestamp | tonumber | ./1000 | strftime("%Y-%m-%dT%H:%M:%SZ")'
```

### Edits

* Remove an item from an array

```bash
jq '.arr1 |= del(.[] | select(. == "foo"))'
```

* Remove all items matchin a regex

```bash
jq '.arr1 |= del(.[] | select(.|test("oo")))'
```

* Multiple deletion command on separate arrays

```bash
jq '.arr1 |= del(.[] | select(.|test("oo"))) | .arr2 |= del(.[]|select(. == "cookie"))'
```

### Create a table view from a json input

Consider an input with the following structure:

```json
[
  {
    "id": "a-123-888888",
    "name": "EntryA",
    "updatedTimestamp": 1571343024191
  },
  {
    "id": "b-234",
    "name": "EntryB",
    "updatedTimestamp": 1706767373652
  },
  {
    "id": "c-456",
    "name": "EntryC",
    "updatedTimestamp": 1683190330454
  }
]
```

To turn this into a table:

```bash
jq -r '.[] | [ .updatedTimestamp, .id, .name ] | @tsv'
``` 

To also display the time in a more readable ISO format:

```bash
jq -r '.[] | [ (.updatedTimestamp | ./1000 | strftime("%Y-%m-%dT%H:%M:%SZ")), .id, .name ] | @tsv'
```

TIP: To align the spaces for a clearer view, pipe the `jq` output to `column -t`
