# How to set up Kubernetes (using k8s playground)

1. Go to [k8s-playground](https://labs.play-with-k8s.com/)
2. Once there, run the following commands in order;

```
kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16
```

The following commands are only for regular users. In the online terminal this won't work:

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Use this instead since you appear to be root
```
export KUBECONFIG=/etc/kubernetes/admin.conf
```

Finally, run the command below:
```
kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml
```

Note: you can use **cntrl + shift + v** to paste in the online terminal.
