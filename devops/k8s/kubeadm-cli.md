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

	 kubeadm init --apiserver-advertise-address=192.40.57.11 --pod-network-cidr=10.244.0.0/16 --apiserver-cert-extra-sans=controlplane --cri-sockert=unix:///var/run/containerd/containerd.sock

	 kubeadm init --apiserver-cert-extra-sans=controlplane --apiserver-advertise-address 192.23.108.8 --pod-network-cidr=10.244.0.0/16 -cri-socket=unix:///var/run/containerd/containerd.sock

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

 							