# hostname
	hostname -f
	hostname -i

# ifconfig
	ifconfig -a

# ip

	ip route
	ip link show cni0
	ip addr
	ip addr show cni0 # (show bridge details along with link show output)

# ipv4/v6 forwarding

	sudo cat /sys/class/dmi/id/product_uuid
	sysctl -w net.ipv6.conf.all.forwarding=1

# iptables
	iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X ipvsadm -C
