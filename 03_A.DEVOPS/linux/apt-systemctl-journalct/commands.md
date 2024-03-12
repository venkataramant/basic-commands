# apt
	sudo apt-get update
	sudo apt-get install -y kubelet kubeadm kubectl
	sudo apt-mark hold kubelet kubeadm kubectl
	apt list kubeadm -a
	apt show kubeadm -b

	uname -a
	cat /etc/lsb-release
    
# systemctl and journalctl
	systemctl daemon-reload
	systemctl restart kubelet
	systemctl status kubelet

# journalctl
	journalctl -u kubelet -f