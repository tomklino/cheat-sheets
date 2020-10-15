# jq

* List paths of all the json file

```bash
cat something.json | jq -c 'path(..)|[.[]|tostring]|join("/")'
```
