# etcdctl commands
export ETCDCTL_API=3

etcdctl \
--cert /etc/kubernetes/pki/etcd/peer.crt \
--key /etc/kubernetes/pki/etcd/peer.key \
--cacert /etc/kubernetes/pki/etcd/ca.crt \
--endpoints https://${HOST0}:2379 endpoint health

snapshot save <<path>>
snapshot status <<path>>
snapshot restore <<path>> -data-dir=<<new_path>>
