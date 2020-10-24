Installing COCKPIT to manage multiple linux servers
Execute below commands on all server you want to manage
yum -y install cockpit
systemctl enable --now cockpit.socket
firewall-cmd --add-service=cockpit
firewall-cmd --add-service=cockpit --permanent

After Cockpit installed successfully, you can access it using a web browser at the following locations.

https://ip-address:9090