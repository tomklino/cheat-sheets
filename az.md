# Azure CLI tool

## Useful --query snippets

* Get all names and prefixes of subnets for a vnet

```
az network vnet show -g "resource-group" -n "vnet" --query 'subnets[].{Name: name, Prefix: addressPrefix}' --output table
```

## Keyvault

* List secrets in a keyvault

```
$ az keyvault secret list --vault-name "keyvault-name"

# Note that a wrong keyvault name will result in the following DNS error:
Max retries exceeded attempting to connect to vault. The vault may not exist or you may need to flush your DNS cache and try again later.
```

* Create a new secret

```
az keyvault secret set --vault-name "keyvault-name" --name "Anannas" --value "Pineapple"
```
