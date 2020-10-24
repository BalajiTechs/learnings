#### Ansible commands
```
ansible --version
ansible web1 -m ping
ssh-keyscan web1
ssh-keyscan lb web1 web2 >> .ssh/known_hosts
cat .ssh/known_hosts
ansible all -m ping --ask-pass
ansible all -m ping
```
	
Established network connections, between ansible server, and client machines.

- Install ntp on inventory group "web1"
```
ansible web1 -m apt -a "name=ntp state=installed" --sudo
```
- Copy a file 
```
ansible web1 -m copy -a "src=/home/vagrant/files/ntp.conf dest=/etc/ntp.conf mode=644 owner=root group=root" --sudo
```
- Restart a service
```
ansible web1 -m service -a "name=ntp state=restarted"ansible all -m shell -a "uptime"
```
- Run uptime on all client machines
```
ansible all -m shell -a "uptime"
```