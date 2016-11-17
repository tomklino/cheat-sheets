# (Chef) knife

A cheat sheet for the chef client knife

```knife search users "groups:sysadmin"```
search in the data bag 'users' for all users containing a value 'sysadmin' in their 'groups' key

```knife ssh "envirnoment:staging" "wall 'hello'"```
run a single time command on all nodes that are part of the staging environment

```knife data bag show users tom```
show the data bag item tom from the users data bag.
(add ```-F json``` at the end to get the response in json)

```knife node show node.fqdn.net```
shows the node in question and its runlist

```knife node edit node.fqdn.net```
fetched the current node's config and loads them in your favorite editor to change at will

```knife role show some-role```
shows the role and the recipes it includes

```knife search environment production```
shows all the nodes from that are part of the production environment

* add a recipe to the run list of a node
```knife node run_list add NODE_NAME RUN_LIST_ITEM (options)
