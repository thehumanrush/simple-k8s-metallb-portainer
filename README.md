# simple-kubernetes-cluster on Ubuntu 22.10  

## Below is ansible-playbook to run
```bash
ansible-playbook site.yml -i inventory/my-k8s/hosts.ini
```

## Change your variable in inventory\my-k8s\group_vars\all.yml & host IP in inventory\my-k8s\hosts.ini