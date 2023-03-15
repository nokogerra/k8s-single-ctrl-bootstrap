## Prepare Ubuntu for k8s bootstrap
This role can prepare your Ubuntu 20.04/22.04 (Focal/Jammy) for k8s cluster bootstrap. Basically it's going to do the following:
- disable UFW;
- configure k8s and docker apt repositories with GPGs (you can add other repos via variable k8s_prep_node_repos);
- disable linux swap;
- install containerd.io, kubeadm, kubectl, kubelet and hold all these packages (you can add other packages);
- load permanently linux kernel modules, required by containerd (you can add other modules);
- enable permanently sysctl parameters, required by containerd (you can add other sysctl parameters);
- create containerd and crictl config files (containerd with SystemdCgroup = true and crictl with runtime endpoint, so you could use it without specifying the endpoint manually);
- enable autocompletion for kubectl, kubeadm and crictl.

For the complete list of variables check main.yml in defaults/.<br />
The main variable you **want** to define is k8s_prep_node_packages:
```
k8s_prep_node_packages:
  - name: "containerd.io"
    version: "1.6.4-1"
  - name: "kubelet"
    version: "1.21.0-00"
  - name: "kubeadm"
    version: "1.21.0-00"
  - name: "kubectl"
    version: "1.21.0-00"
```
For an example check tests/.