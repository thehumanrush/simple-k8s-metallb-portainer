# simple-kubernetes-cluster on Ubuntu 22.10  
  
  
apt install docker.io -y  
apt install apt-transport-https curl -y  
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add  
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list  
apt update  
apt install -y kubeadm=1.23.17-00 kubelet=1.23.17-00 kubectl=1.23.17-00 kubernetes-cni=1.1.1-00  
  
  
run below on master only  
==========  
kubeadm init --pod-network-cidr=192.168.0.0/16  
mkdir -p $HOME/.kube  
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config  
chown $(id -u):$(id -g) $HOME/.kube/config  
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/tigera-operator.yaml  
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/custom-resources.yaml  
  
then run join  
==========  
kubeadm join \<ip address\>:6443 --token \<token\> \  
--discovery-token-ca-cert-hash \<sha256 hash\>  
  
