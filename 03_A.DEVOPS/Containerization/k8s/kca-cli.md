#	kubectl commands
**proxy**

kubectl --kubeconfig ./admin.conf proxy http://localhost:8001/api/v1

#							kubeadm commands
	sudo kubeadmin init
	sudo kubeadm init --control-plane-endpoint "LOAD_BALANCER_DNS:LOAD_BALANCER_PORT" --upload-certs
	sudo kubeadm init phase upload-certs --upload-certs # Reupload the certificates
	sudo kubeadm reset
	kubeadm kubeconfig user --org system:nodes --client-name system:node:$NODE > kubelet.conf. 
	kubeadm token list
	kubeadm token create
	kubeadm config print init-defaults --component-configs KubeletConfiguration

	kubeadm init --pod-network-cidr=10.244.0.0/16,2001:db8:42:0::/56 --service-cidr=10.96.0.0/16,2001:db8:42:1::/112

  kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>

  kubeadm certs certificate-key
  sudo kubeadm join <control-plane-host>:<control-plane-port> --token <token>  --discovery-token-ca-cert-hash sha256:<hash> --control-plane --certificate-key <certificatekey>


  for ca-cert-hash
	openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \
   openssl dgst -sha256 -hex | sed 's/^.* //'

	kubeadm init phase certs etcd-ca

	kubeadm kubeconfig user 
	kubeadm kubeconfig user --client-name <CN> 
	kubectl create (cluster)rolebinding
Create certificates for each member.

	kubeadm init phase certs etcd-server --config=/tmp/${HOST2}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-peer --config=/tmp/${HOST2}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-healthcheck-client --config=/tmp/${HOST2}/kubeadmcfg.yaml
	kubeadm init phase certs apiserver-etcd-client --config=/tmp/${HOST2}/kubeadmcfg.yaml
	cp -R /etc/kubernetes/pki /tmp/${HOST2}/
	# cleanup non-reusable certificates
	find /etc/kubernetes/pki -not -name ca.crt -not -name ca.key -type f -delete

	kubeadm init phase certs etcd-server --config=/tmp/${HOST1}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-peer --config=/tmp/${HOST1}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-healthcheck-client --config=/tmp/${HOST1}/kubeadmcfg.yaml
	kubeadm init phase certs apiserver-etcd-client --config=/tmp/${HOST1}/kubeadmcfg.yaml
	cp -R /etc/kubernetes/pki /tmp/${HOST1}/
	find /etc/kubernetes/pki -not -name ca.crt -not -name ca.key -type f -delete

	kubeadm init phase certs etcd-server --config=/tmp/${HOST0}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-peer --config=/tmp/${HOST0}/kubeadmcfg.yaml
	kubeadm init phase certs etcd-healthcheck-client --config=/tmp/${HOST0}/kubeadmcfg.yaml
	kubeadm init phase certs apiserver-etcd-client --config=/tmp/${HOST0}/kubeadmcfg.yaml
	# No need to move the certs because they are for HOST0

	# clean up certs that should not be copied off this host
	find /tmp/${HOST2} -name ca.key -type f -delete
	find /tmp/${HOST1} -name ca.key -type f -delete

*services to use the subnet 10.96.0.0/12 as the default for services, you can pass the --service-cidr*
	kubeadm init --service-cidr 10.96.0.0/12

From a working control plane node in the cluster that has /etc/kubernetes/pki/ca.key execute kubeadm kubeconfig user --org system:nodes --client-name system:node:$NODE > kubelet.conf. $NODE must be set to the name of the existing failed node in the cluster. Modify the resulted kubelet.conf manually to adjust the cluster name and server endpoint, or pass kubeconfig user --config (it accepts InitConfiguration). If your cluster does not have the ca.key you must sign the embedded certificates in the kubelet.conf externally.

# kubelet comamnds
	systemctl restart kubelet
	--node-ip
	systemctl daemon-reload
	systemctl restart kubelet

 							
#	kubectl commands
**proxy**

kubectl --kubeconfig ./admin.conf proxy
	http://localhost:8001/api/v1

**config**
	kubectl config delete-cluster

**node**
	kubectl drain <node name> --delete-emptydir-data --force --ignore-daemonsets
	kubectl delete/describe node <node name>

**logs**

**get**

kubectl get pods --all-namespaces

kubectl logs myapp-pod -c init-myservice # Inspect the first init container
kubectl logs myapp-pod -c init-mydb      # Inspect the second init container


**get::pods**

kubectl get pods --all-namespaces

**get::field-selector**

kubectl get pods --field-selector status.phase=Running

kubectl get services  --all-namespaces --field-selector metadata.namespace!=default

kubectl get pods --field-selector=status.phase!=Running,spec.restartPolicy=Always

**get:events**

kubectl get events -A --field-selector=reason=OwnerRefInvalidNamespace

**get:lease**
kubectl -n kube-system get lease -l apiserver.kubernetes.io/identity=kube-apiserver


**labels**

kubectl get pods -l app=nginx -L tier
-L or --label-columns

kubectl label pods -l app=nginx tier=fe

k label node node01 color=blue
k get nodes --show-labels

**services***
kubectl create service clusterip echoserver --tcp=80:8080
kubectl create service nodeport echoserver --tcp=5005:8080
kubectl create service loadbalancer echoserver --tcp=5005:8080

kubectl run echoserver --image=k8s.gcr.io/echoserver:1.10 --restart=Never \
  --port=8080 --expose
kubectl expose deployment echoserver --port=80 --target-port=8080

kubectl run tmp --image=busybox --restart=Never -it --rm \
  -- wget 10.96.254.0:5005
 


**namespaces**
	
	kubectl get namespace
	kubectl run nginx --image=nginx --namespace=<insert-namespace-name-here>
	kubectl get pods --namespace=<insert-namespace-name-here>

	kubectl config set-context --current --namespace=<insert-namespace-name-here>
	kubectl config view --minify | grep namespace:
	
	# In a namespace
	kubectl api-resources --namespaced=true

	# Not in a namespace
	kubectl api-resources --namespaced=false


**nodes***
kubectl get nodes minikube -o json | jq .spec.podCIDR
kubectl get nodes -o \
  jsonpath='{ $.items[*].status.addresses[?(@.type=="InternalIP")].address }'

kubectl get nodes -o jsonpath='{..status.addresses[?(@.type=="InternalIP")].address}'
k get nodes -o=jsonpath="{range .items[*]}{.metadata.name}{'\t'}{.status.addresses[?(@.type=='InternalIP')].address}{'\t'}{end}"


**nodes:taints**
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
node.kubernetes.io/not-ready:NoSchedule

**set**

kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1 --record

**taints**

kubectl taint nodes --all node-role.kubernetes.io/control-plane-
node.kubernetes.io/not-ready:NoSchedule


**Deployments**

*Cannot rollback a paused Deployment until you resume it.*
```
kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml


kubectl get pods --show-labels


kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1

kubectl set resources deployment/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi
kubectl edit deployment/nginx-deployment
kubectl scale deployment/nginx-deployment --replicas=10
kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80

kubectl set resources deployment/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi


**Deployments**

*Cannot rollback a paused Deployment until you resume it.*
```
kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
kubectl get pods --show-labels


kubectl get rs -w

**Advance**
kubectl -n kube-system get deployment coredns -o yaml | \

kubectl get rs -w

Advance
	kubectl -n kube-system get deployment coredns -o yaml | \

  sed 's/allowPrivilegeEscalation: false/allowPrivilegeEscalation: true/g' | \
  kubectl apply -f -
```
**Deployments:Patch**
kubectl patch deployment/nginx-deployment -p '{"spec":{"progressDeadlineSeconds":600}}'

.spec.revisionHistoryLimit/10
.spec.template.spec.restartPolicy true
.spec.replicas 1
.spec.selector must match .spec.template.metadata.labels, or it will be rejected by the API.
.spec.strategy   "Recreate" or "RollingUpdate"
.spec.progressDeadlineSeconds /600
.spec.minReadySeconds.
.spec.paused



  kubectl -n kube-system patch ds kube-proxy -p='{ "spec": { "template": { "spec": { "tolerations": [ { "key": "CriticalAddonsOnly", "operator": "Exists" }, { "effect": "NoSchedule", "key": "node-role.kubernetes.io/control-plane" } ] } } } }'


**Deployments:Rollout**
kubectl rollout status deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment --revision=2

kubectl rollout undo deployment/nginx-deployment

kubectl rollout undo deployment/nginx-deployment --to-revision=2
kubectl rollout status deployment/nginx-deployment

kubectl rollout pause deployment/nginx-deployment

kubectl rollout history deployment/nginx-deployment

kubectl rollout resume deployment/nginx-deployment

kubectl -n kube-system rollout restart deployment coredns

kubectl rollout status deployment/nginx-deployment

**replicasets**

kubectl autoscale rs frontend --max=10 --min=3 --cpu-percent=50

**hpa**
kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
k get hpa

**exec**

kubectl exec pod/mypod -- cat /log/my.log
kubectl exec -it pod/mypod -- id

**configmap**

**secrets**
k create secret generic api-basic-auth -n secure --from-literal=username=bot --from-literal=password=pa88w0rD --type=kubernetes.io/basic-auth -o yaml --dry-run=client

k create secret generic api-basic-auth -n secure --from-literal=username=bot --from-literal=password=pa88w0rD --type=kubernetes.io/basic-auth

k create secret generic secret-ssh-auth -n mygic --type=kubernetes.io/ssh-auth --from-file=ssh-privatekey=/root/.ssh/id_rsa

k describe secret/secret-ssh-auth -n mygic

kubectl get secret secret-ssh-auth -n mygic -o json | jq '.data."ssh-privatekey"' -r

**ingress**
k get ingress
kubectl create ingress myingress  --rule="mypath1/path2/path3=corellian:8080"

curl -H "Host: cka.mylocal.com" x.y.z.100

kubectl get ingress corellian --output=jsonpath="{.status.loadBalancer.ingress[0][ip]}"
k describe/edit ingress/<<ingress-name>>

**ingress-controller**
k create ns ingress-nginx
  # Need one ConfigMap
k create configmap ingress-nginx-controller  -n ingress-nginx
  # Need two ServiceAccounts
k create sa ingress-nginx-admission -n ingress-nginx
k create sa ingress-nginx -n ingress-nginx

** jsonpath**
k get nodes -o=jsonpath={.items[*].metadata.name} > /opt/outputs/node_names.txt
k get nodes --sort-by metadata.name -o custom-columns=Name:.metadata.name
k get nodes -o=jsonpath="{range .items[*]}{.status.nodeInfo.osImage}{end}" > /opt/outputs/nodes_os.txt
k get nodes -o json | jq .items[].status.nodeInfo.osImage
k get nodes -o=jsonpath="{range .items[*]}{.status.nodeInfo.osImage}{'\n'}{end}"
k get pv --sort-by=.spec.capacity.storage > /opt/outputs/storage-capacity-sorted.txt
k get pv --sort-by=.spec.capacity.storage -o custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage > /opt/outputs/pv-and-capacity-sorted.txt

kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}" > /opt/outputs/aws-context-name

 k get nodes -o json |  jq '.items[].status.addresses[]| select(.type=="InternalIP").address'

**static pods***

kubectl run -n networking --restart=Never --image=busybox static-busybox --dry-run=client -oyaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml

kubectl run -n networking --restart=Never --image=busybox busybox   -it --rm -- /bin/sh

**service account**
k create sa my-sa1
 k create token my-sa1

**SA to call APIs**
kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}'
https://172.x.y.z:6443

kubectl get serviceaccount api-access -n apps -o jsonpath='{.secrets[0].name}'

token=`kubectl get secret $(kubectl get serviceaccount api-access -n apps -o jsonpath='{.secrets[0].name}') -o jsonpath='{.data.token}' -n apps | base64 --decode`

k_server=`kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}'`

kubectl exec operator -n apps -- curl ${k_server}/api/v1/namespaces/rm/pods --insecure  --header "Authorization: Bearer ${token}"

kubectl exec operator -n apps -- curl ${k_server}/api/v1/namespaces/apps/pods --insecure  --header "Authorization: Bearer ${token}"

kubectl exec operator -n apps -- curl  -X GET ${k_server}/api/v1/namespaces/rm/pods/disposable --insecure  --header "Authorization: Bearer ${token}"

kubectl exec operator -n apps -- curl  -X GET ${k_server}/api/v1/namespaces/apps/pods/mynginx --insecure  --header "Authorization: Bearer ${token}"


kubectl exec operator -n apps -- curl -X DELETE ${k_server}/api/v1/namespaces/rm/pods/disposable --insecure  --header "Authorization: Bearer ${token}"

kubectl exec operator -n apps -- curl -X DELETE ${k_server}/api/v1/namespaces/apps/pods/mynginx --insecure  --header "Authorization: Bearer ${token}"

**csr certificate**

k certificate approve my-csr1
k certificate deny my-csr2
k delete csr/my-csr2
k get csr/my-csr2


**clusterroles and bindings**
k create clusterrole service-view --verb="get,list" --resource="services"
k create clusterrole service-view --verb=get,list --resource=services

k create clusterrolebinding myuser-service-view --clusterrole=service-view --user=myuser -n development -o yaml --dry-run=client
k create clusterrolebinding myuser-service-view --clusterrole=service-view --user=myuser -n development

kubectl create clusterrole aggregate-combined --aggregation-rule="rbac.cka.cncf.com/aggregate=true"

kubectl create clusterrole dep-modify --verb=create,delete,patch,update --resource=deployments --dry-run=client -o yaml

kubectl create serviceaccount pvviewer
kubectl create clusterrole pvviewer-role --resource=persistentvolumes --verb=list
kubectl create clusterrolebinding pvviewer-role-binding --clusterrole=pvviewer-role --serviceaccount=default:pvviewer

**top**
k top pod --sort memory
k top pod --sort cpu
k top node

**Helm**

helm package .


**kustomization***
k kustomize . # refer kustomization.yaml and pod.yaml

# busybox Interactive

k run busybox --image=busybox -n other -it --rm -- /bin/sh


# etcdctl commands

ETCDCTL_API=3 etcdctl \
--cert /etc/kubernetes/pki/etcd/peer.crt \
--key /etc/kubernetes/pki/etcd/peer.key \
--cacert /etc/kubernetes/pki/etcd/ca.crt \
--endpoints https://${HOST0}:2379 endpoint health

