# Azure CLI tool

## Useful --query snippets

* Get all names and prefixes of subnets for a vnet

```
az network vnet show -g "resource-group" -n "vnet" --query 'subnets[].{Name: name, Prefix: addressPrefix}' -otable
```

* List secrets along with their URL

```
az keyvault secret list --vault-name "keyvault-name" --query "[].{Name: name, url: id}" -otable
```

## Keyvault

* List secrets in a keyvault

```
az keyvault secret list --vault-name "keyvault-name"

# Note that a wrong keyvault name will result in the following DNS error:
Max retries exceeded attempting to connect to vault. The vault may not exist or you may need to flush your DNS cache and try again later.
```

* Create a new secret

```
az keyvault secret set --vault-name "keyvault-name" --name "Anannas" --value "Pineapple"
```

* Show access policies for keyvault

```
az keyvault show --name "keyvault-name" --query "properties.accessPolicies"
```

* Add permissions to an object to list and get keys

```
az keyvault set-policy --name toklino-contoso-keyvault --object-id 8abcd500-523c-4d00-9c5d-90b7fffbea0b --secret-permissions list get

# Where the object id is the unique identifier of the object, for example, for a webapp, can be obtained as such:
az webapp show --name toklinov-webapp --resource-group toklinov-rg --query identity.principalId -o tsv
```

* Get the URI of a secret (to be used in configuration of services that need to consume the secret)

```
az keyvault secret show --vault-name keyvault-name --name StorageAccount --query "id"

# Or, directly into a variable (note the -otsv at the end):
storageAccountSecretUri=$(az keyvault secret show --vault-name keyvault-name --name StorageAccount --query "id" -otsv)
```

## Webapps (app service)

```
* List webapps
az webapp list -otable
```

* Get unique object id of webapp for use with keyvault permissions

```
# NOTE the '-o tsv' is important if you want to place the output into a variable, without it the output will come out with quotes
az webapp show --name toklinov-webapp --resource-group toklinov-rg --query identity.principalId -o tsv
```

* Set configurations for webapp

```
# set a connection string based on a secret in keyvault (see the keyvault section for how to set the variable in the example)

az webapp config connection-string set \
  -g resource-group-name -n webapp-name \
  -t Custom --settings "StorageAccount=@Microsoft.KeyVault(SecretUri=${storageAccountSecretUri})"
```
