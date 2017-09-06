# Chef and knife

## knife common

* search in the data bag 'users' for all users containing a value 'sysadmin' in their 'groups' key

```bash
knife search users "groups:sysadmin"
```

* a hack to organise `knife search node` results as `knife node list`

```bash
knife search node "environment:production" -a name | grep -Ev "^[\ ]" | sed '/^\s*$/d' | cut -d ":" -f1
```

* run a single time command on all nodes that are part of the staging environment

```bash
knife ssh "envirnoment:staging" "wall 'hello'"
```

* show the data bag item tom from the users data bag.
(add ```-F json``` at the end to get the response in json)

```bash
knife data bag show users tom
```

* show the node in question and its runlist

```bash
knife node show node.fqdn.net
```

* fetch the current node's config and loads them in your favorite editor to change at will

```bash
knife node edit node.fqdn.net
```

* show the role and the recipes it includes

```bash
knife role show some-role
```

* show all the nodes from that are part of the production environment

```bash
knife search environment production
```

* add a recipe to the run list of a node

```bash
knife node run_list add NODE_NAME RUN_LIST_ITEM (options)
```

* search nodes running a specific recipe

```bash
knife search node 'recipes:cookbook\:\:recipe'
```

## chef tricks

* quick way to get the actual value of an attribute in chef remotely

```bash
ssh node.fqdn.com "printf \"node['some']['attribute']\\nexit\\n\" | sudo chef-shell -z 2>/dev/null | awk 'BEGIN{f=0}; /^chef/{f=1} {if(f) print}'"
```

* a neat way to check a recipe change on a single server without actually updating it

```bash
echo "$USER: testing recipe";
#edit your cookbook in /var/chef/cache/cookbooks and then continue to the following line
lockreason="$(cat /tmp/chef.lock) && rm /tmp/chef.lock && chef-client --skip-cookbook-sync; echo $lockreason > /tmp/chef.lock
```
