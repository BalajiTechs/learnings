HA using Pacemaker and Corosync
Node 1
	yum install pcs
	systemctl enable pcsd.service corosync pacemaker
	systemctl start pcsd.service
	
	Installation creates user hacluster so need to reset password 
	passwd hacluster
	
Node 2
	yum install pcs 
	systemctl enable pcsd.service corosync pacemaker
	systemctl start pcsd.service
	
Installation creates user hacluster so need to reset password
	passwd hacluster
	
Add Constraint to start both resorces on same machine
	pcs constraint colocation add VirtualIP LDS_INSTANCE


After installation pacemaker any one node
	pcs cluster auth node1 node2

Note: If auth fails then check if password for the hacluster is same on all nodes. Also check if nodes are connected. Check firewall not blocking 2224 port. Check pcsd is running on all nodes. Try using FQDN instead of just hostname.

Execute below command on any node to setup cluster
	pcs cluster setup --name mycluster node1 node2 

	pcs cluster enable --all	


See Full configration of pcs
	pcs cluster cib


Add a Resource IP
pcs resource create ClusterIP ocf:heartbeat:IPaddr2 ip=<any Free IP on network> cidr_netmask=32 op monitor interval=30s

Reference
http://clusterlabs.org/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/ch03.html