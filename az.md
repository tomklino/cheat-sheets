# Azure CLI tool

## General Pupose

* Show active account and subscription

```
az account show -otable
```

* List registered accounts and subscriptions

```
az account list -otable
```

* Switch subscription

```
az account set --subscription "My Demos"
```

## Useful --query snippets

* Get all names and prefixes of subnets for a vnet

```
az network vnet show -g "resource-group" -n "vnet" --query 'subnets[].{Name: name, Prefix: addressPrefix}' -otable
```

* List secrets along with their URL

```
az keyvault secret list --vault-name "keyvault-name" --query "[].{Name: name, url: id}" -otable
```

## VMs

* Create a vm:

```
az vm create -g resource-group --name hostname1 \
  --size Standard_B1ls --vnet-name vnet-of-choice --ssh-key-values ~/.ssh/id_rsa.pub \
  --image Canonical:UbuntuServer:18.04-LTS:18.04.202006101
```

* To get a list of possible sizes to use:

```
# replace westeurope with the location of your choice
az vm list-sizes -l westeurope -otable
```

* To get a list of images:

```
# Common publishers are: OpenLogic, CoreOS, Debian, SUSE, RedHat, SUSE, Canonical
az vm image list --publisher canonical --all -otable
```

* Get the public IP of a VM by name

```
az vm show -d -g resource-group -n hostname1 --query "publicIps" -otsv
```

## Network

* List public IPs

```
az network public-ip list -otable
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


* List webapps

```
az webapp list -otable
```

* Get the URL of a webapp

```
az webapp show -g resource-group-name -n webapp-name --query "defaultHostName" -otsv
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
