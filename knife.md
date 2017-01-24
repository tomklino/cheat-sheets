# (Chef) knife

## A cheat sheet for the chef client knife

* search in the data bag 'users' for all users containing a value 'sysadmin' in their 'groups' key

```knife search users "groups:sysadmin"```

* run a single time command on all nodes that are part of the staging environment

```knife ssh "envirnoment:staging" "wall 'hello'"```

* show the data bag item tom from the users data bag.
(add ```-F json``` at the end to get the response in json)

```knife data bag show users tom```

* show the node in question and its runlist

```knife node show node.fqdn.net```

* fetch the current node's config and loads them in your favorite editor to change at will

```knife node edit node.fqdn.net```

* show the role and the recipes it includes

```knife role show some-role```

* show all the nodes from that are part of the production environment

```knife search environment production```

* add a recipe to the run list of a node

```knife node run_list add NODE_NAME RUN_LIST_ITEM (options)```

* search nodes running a specific recipe

```knife search node 'recipes:cookbook\:\:recipe'```
