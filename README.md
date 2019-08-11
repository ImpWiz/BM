# BM
---
Create secure cloud infrastructure

https://www.datawire.io/guide/infrastructure/setting-kubernetes-aws/



## MASTER

``` console

set -o vi
sudo yum -y update && sudo yum -y install epel-release
sudo cp /etc/selinux/config /etc/selinux/config.`date +%d%b%Y.%H%M%S`
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
swapoff -a
ls /etc/selinux/config*
cksum /etc/selinux/config*
diff `ls /etc/selinux/config*`
sudo reboot
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum update
yum -y install docker-ce docker-ce-cli containerd.io

yum install -y yum-utils device-mapper-persistent-data lvm2

# This shows Available Docker Versions
yum list docker-ce --showduplicates | sort -r

# >> >> >>  kubernetes.repo (( File Under <> Code ))
vi /etc/yum.repos.d/kubernetes.repo

yum update
yum install -y kubelet kubeadm kubectl

# This Starts Docker
systemctl start docker

# This enables Docker to Start at Boot
systemctl enable docker


# This will start Kubernetics, and it is ok if it fails
systemctl start kubelet

# This Allows Kerbentics to run at Boot
systemctl enable kubelet

sudo kubeadm init 
kubectl get nodes

# To start using your cluseter, you will need to run the following as a regular user
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

systemctl status docker
systemctl status kubelet

# <IF> Token is not on screen run this command to create a join token for workers
# >> kubean init


modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables

vi /etc/hosts
172.31.35.243  master
172.31.41.0   worker

vi /etc/sysconfig/network
- - - - - 
HOSTNAME=master
- - - - - 


```
---
## Worker Config
---

vi /etc/hostname
vi /etc/hosts




# How to open ports in aws security group
``` console
aws ec2 authorize-security-group-ingress --group-name imubit --protocol tcp --port 10251 --cidr 0.0.0.0/0
```

---
### https://www.tutorialkart.com/bash-shell-scripting/bash-date-format-options-examples/
``` console
sudo cp /etc/selinux/config /etc/selinux/config.`date +%d%b%Y.%H%M%S`
ls /etc/selinux/config*
cksum /etc/selinux/config*

sudo vim /etc/selinux/config

# In this file change  SELINUX=enforcing
#   change SELINUX=enforcing
#   to 
#   SELINUX=disabled

sudo reboot

diff `ls /etc/selinux/config*`
```

## - Kubernetes based stack for running applications

### https://www.howtoforge.com/tutorial/centos-kubernetes-docker-cluster/

``` console
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
sudo swapoff -a
vim /etc/fstab
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum update 
yum install -y docker-ce
```

--- 
### https://myopswork.com/how-to-install-kubernetes-k8-in-rhel-or-centos-in-just-7-steps-2b78331174a5

``` console
vim /etc/yum.repos.d/kubernetes.repo
# [kubernetes]


sudo yum update 
sudo yum install -y kubelet kubeadm kubectl
sudo reboot
sudo systemctl start docker && sudo systemctl enable docker
sudo systemctl start kubelet && sudo systemctl enable kubelet
sudo systemctl status docker && sudo systemctl status kubelet
sudo docker info | grep -i cgroup
sudo docker ps
sudo docker images
sudo docker search centos
set -o vi
sed -i 's/cgroup-driver=systemd/cgroup-driver=cgroupfs/g' /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
```

--- 
### https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-cluster-using-kubeadm-on-centos-7

. . . . . . . 
 
