# Install free5gc

Enable more cgroup control for minikube
```bash
$ sudo vim /etc/default/grub # GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
$ sudo update-grub
```

Set up the VMs
```bash
# install docker
# install minikube
# install helm
$ minikube start --driver=virtualbox --network-plugin=cni --cni=flannel --memory 12288 --cpus 6
$ minikube start --driver=docker --network-plugin=cni --cni=flannel --memory 12288 --cpus 6
$ minikube docker-env # to helm with minikube
# add alias kubectl="minikube kubectl --" to .bashrc
```

Install gtp5g module
```bash
$ sudo apt update
$ sudo apt install gcc make build-essential
$ git clone https://github.com/free5gc/gtp5g.git
$ cd gtp5g
$ make
$ sudo make install
```

Install MULTUS
```bash
$ kubectl apply -f https://raw.githubusercontent.com/k8snetworkplumbingwg/multus-cni/master/deployments/multus-daemonset-thick-plugin.yml
```

Add helm repo
```bash
$ helm repo add towards5gs 'https://raw.githubusercontent.com/Orange-OpenSource/towards5gs-helm/main/repo/'
$ helm repo update
```

Create two networks in minikube
```bash
$ minikube ssh
$ sudo ip link add eth00 link eth0 type macvlan mode bridge
$ sudo ip link add eth11 link eth0 type macvlan mode bridge

$ sudo ip addr add 10.100.50.1/24 brd + dev eth00
$ sudo ip addr add 10.100.100.1/24 brd + dev eth11

$ sudo ip link set eth00 up
$ sudo ip link set eth11 up

$ sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

$ grep -rl eth0 . | xargs sed -i 's/eth0/eth00/g'
$ grep -rl eth1 . | xargs sed -i 's/eth1/eth11/g'

$ cd towards5gs-helm/charts
$ helm install free5gc ./freeg5c

# login in to free5gc-webgui (port 30050), username: admin, psssword: free5gc 
$ ssh -L 30500:192.168.49.2:30500 _rise_mine
# create a new subscriber
# edit ueransim helm chart values
$ vim towards5gs-helm/charts/ueransim/values.yaml
$ helm install ueransim ./ueransim
```
