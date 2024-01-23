1. Configure libvirtd

sudo system status libvirtd
brew services start/status libvirtd
brew 

virt-manager/virt-install/virt-clone/virsh/

(Graphical interface for libvirtd)
virt-manager  [ looks for system]

virsh list -all [ looking for user]
virsh net-start default
virsh shutdown 1 or name
virsh network address?

qemu groups
qemu:///system
qemu:///user (root less mode)

# Permissions

/etc/libvirt/libvirt.conf
~/.config/libvirt/

qemu:///system, access is dictated by "polkit"

1. add user to the polkit group
2. create a sudo group and add user to sudo group and add sudo  to "vish or virt-manager" commands
3. add sudo group to polkit config

/etc/polkit-1/rules.d/50-libvirt.rules

/* allow users in abcd group to manage the libvirt daemon without authenication"

polkit.addRule(function(action,subject){
	if (action.id=="org.libvirt.unix.manage" && subject.isInGroup("abcd")){
			return polkit.Result.YES;
	}
}
	
});



# creating a virtual machine
/var/lib/libvirt
--- images (images are stored qcow2) 
--- isos (server installation disk)

ido



/usr/local/Cellar/libvirt
/usr/local/etc/libvirt/libvirtd.conf
/usr/local/opt/libvirt/sbin/libvirtd 


/usr/local/Cellar/virt-manager/4.1.0.4


qeumu-img create -f qcow2 ubuntu.qcow2 50g


qemu:///system
qemu:///user (root less mode)


