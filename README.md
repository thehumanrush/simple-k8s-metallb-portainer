# simple-kubernetes-cluster on Ubuntu 22.10  
  
Run below on both master and worker :  
==========
```bash
apt install docker.io -y
apt install apt-transport-https curl -y
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
apt update
apt install -y kubeadm=1.23.17-00 kubelet=1.23.17-00 kubectl=1.23.17-00 kubernetes-cni=1.1.1-00
apt-mark hold kubelet kubeadm kubectl
```
  
run below on master only :  
==========
```bash
kubeadm init --pod-network-cidr=192.168.0.0/16
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/tigera-operator.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/custom-resources.yaml
```

then run join on worker :  
==========  
```bash
kubeadm join <ip address>:6443 --token <token> \
--discovery-token-ca-cert-hash <sha256 hash>
```


Use below cert-Manager for Rancher  
==========
```bash
apply -f https://github.com/jetstack/cert-manager/releases/download/v1.4.0/cert-manager.yaml
```
