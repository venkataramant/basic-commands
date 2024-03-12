# Disable Swap
    sudo swapoff -a

# Linux Network
    ip link 
    ifconfig -a
    ip addr show
    sudo cat /sys/class/dmi/id/product_uuid
    sysctl -w net.ipv6.conf.all.forwarding=1
    
# iptables
    iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X
    ipvsadm -C

# systemctl and journalctl
    systemctl daemon-reload
    systemctl restart kubelet
    systemctl status kubelet

# kubectl
    sudo apt-get update
    sudo apt-get install -y kubelet kubeadm kubectl
    sudo apt-mark hold kubelet kubeadm kubectl

# TLS commands
	openssl x509 -text -noout
	openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt 
	openssl rsa -pubin -outform der 
	openssl dgst -sha256 -hex
	
	openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \
	   openssl dgst -sha256 -hex | sed 's/^.* //'

# env variable
	unset KUBECONFIG
	export KUBECONFIG=/etc/kubernetes/admin.conf
	sudo -E -s

# sed
	sed 's/allowPrivilegeEscalation: false/allowPrivilegeEscalation: true/g'
	sed 's/^.* //'


