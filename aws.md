# aws cli tool

## DNS (Route53)

* List records:

```bash
# First, list hosted zones:

aws route53 list-hosted-zones # Optional pipe: jq '.HostedZones[].Id'

# Then, for each zone:
aws route53 list-resource-record-sets --hosted-zone-id /hostedzone/XXXXXXXX
```
