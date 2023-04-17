# simple-kubernetes-cluster on Ubuntu 22.10  

## Change your variable in 
```bash
inventory\my-k8s\group_vars\all.yml
```
and host IP in
```bash
inventory\my-k8s\hosts.ini
```

## Below is ansible-playbook to run
```bash
ansible-playbook site.yml -i inventory/my-k8s/hosts.ini
```
