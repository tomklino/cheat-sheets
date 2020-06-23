# Azure CLI tool

## Useful --query snippets

* Get all names and prefixes of subnets for a vnet

```
az network vnet show -g "resource-group" -n "vnet" --query 'subnets[].{Name: name, Prefix: addressPrefix}' --output table
```
