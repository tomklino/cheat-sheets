# aws cli tool

## DNS (Route53)

* List records:

```bash
# First, list hosted zones:

aws route53 list-hosted-zones # Optional pipe: jq '.HostedZones[].Id'

# Then, for each zone:
aws route53 list-resource-record-sets --hosted-zone-id /hostedzone/XXXXXXXX
```

* All route53 A and CNAME records in one command:

```bash
aws route53 list-hosted-zones | \
  jq '.HostedZones[].Id' | tr -d '"' | \
  while read zone; do \
    aws route53 list-resource-record-sets --hosted-zone-id $zone | \
    jq '.ResourceRecordSets[] | select(.Type == "A" or .Type == "CNAME") | .Name' | \
    tr -d '"'; \
  done
```
