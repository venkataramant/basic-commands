On the controlplane node, run the following set of commands to deploy the network plugin:
Download the original YAML file and save it as kube-flannel.yml:
curl -LO https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
Open the kube-flannel.yml file using a text editor.

Locate the args section within the kube-flannel container definition. It should look like this:

  args:
  - --ip-masq
  - --kube-subnet-mgr
Add the additional argument - --iface=eth0 to the existing list of arguments.

Now apply the modified manifest kube-flannel.yml file using kubectl:

kubectl apply -f kube-flannel.yml
After applying the manifest, the STATUS of both the nodes should become Ready

controlplane ~ ➜  kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   15m   v1.27.0
node01         Ready    <none>          15m   v1.27.0

# weave

https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml


 - name: IPALLOC_RANGE
>  value: 10.32.1.0/24
----------------------------------------------------------------
https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
 args:
  - --ip-masq
  - --kube-subnet-mgr
  Add
  - --iface=eth0
----------------------------------------------------------------------------------------

https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml

https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

raw.githubusercontent.com -- github.com
flannel-io                -- weaveworks
flannel					  -- weave
-                         -- releases/download

v0.20.2					  -- v2.8.1
Documentation			  -- -

kube-flannel.yml          -- weave-daemonset-k8s.yaml

yml						  -- yaml

 