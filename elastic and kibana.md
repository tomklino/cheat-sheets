# Elasticsearch

* Quick command to release read only lock after disk space got full:

```bash
curl -X PUT \
  -H "Content-Type: application/json" \
  elasticsearch:9200/_all/_settings \
  -d '{"index.blocks.read_only_allow_delete": null}'
```
