--------------------------------------------------------------------------------------------------
cloud-init install
yum install cloud-init
install ovirt-guest Using YUM via terminal to install the oVirt Guest Tools
	sudo yum install centos-release-ovirt42
	sudo yum install ovirt-guest-agent-common
Starting the service
	sudo systemctl enable --now ovirt-guest-agent.service

--------------------------------------------------------------------------------------------------
Create a user on ovirt-engine
ovirt-aaa-jdbc-tool user add dhirendrap --attribute=firstName=dhirendra --attribute=lastName=pratap
ovirt-aaa-jdbc-tool user password-reset dhirendrap

--------------------------------------------------------------------------------------------------
Configuring NFS Shared Storage on the oVirt Node
 Procedure

Create the shared directories.

# mkdir -p /export/nfs/data /export/nfs/iso

Adjust the file permissions.

# chown vdsm:kvm /export/nfs/data /export/nfs/iso

Create the NFS export file.

Edit the file /etc/exports with the following content:

# cat /etc/exports
/export/nfs/data *(rw,no_subtree_check,insecure,no_root_squash)
/export/nfs/iso *(rw,no_subtree_check,insecure,no_root_squash)

Set the appropriate permissions to the shared directories:

# chmod 0755 /export/nfs/data/ 
# chmod 0755 /export/nfs/iso/

The directory owner, you, have permission to read, write, and execute, which is designated with the number 7. Other users can read and execute but not write, which is designated with the number 5.
Enable the export directories as active NFS mount points.

# exportfs -a
# systemctl enable nfs-server
# systemctl start nfs-server
# showmount -e localhost

The shared directories are ready to be used as data domains for the data center.