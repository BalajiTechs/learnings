Vagrant commands
#install on centos 7
curl https://releases.hashicorp.com/vagrant/2.1.5/vagrant_2.1.5_x86_64.rpm >> vagrant.rpm
rpm -ivh vagrant.rpm
-------------------------------------------------------------------------------------------------
#Installing ovirt-provider
# Vagrant 1.8+ is must(https://www.vagrantup.com/downloads.html)
# references https://github.com/myoung34/vagrant-ovirt4
# $ yum -y install gcc libcurl-devel libxml2-devel redhat-rpm-config ruby ruby-devel rubygems rubygems-devel
# $ vagrant plugin install vagrant-ovirt4
# $ vagrant up --provider=ovirt4


Vagrant.configure("2") do |config|
  config.vm.box = 'ovirt4'
  config.vm.hostname = "vagrant-test"
  config.vm.box_url = 'https://github.com/myoung34/vagrant-ovirt4/blob/master/example_box/dummy.box?raw=true'

  config.vm.provider :ovirt4 do |ovirt|
    ovirt.url = 'https://ovirt-mgmt.example.in/ovirt-engine/api'
    ovirt.username = "admin@internal"
    ovirt.password = "password"
    ovirt.insecure = true
    ovirt.debug = true
    ovirt.cluster = 'Apollo'
    ovirt.template = 'vagrant-centos7'
    ovirt.console = 'spice'
    ovirt.memory_size = '1 GiB' #see https://github.com/dominikh/filesize for usage
    ovirt.memory_guaranteed = '256 MB' #see https://github.com/dominikh/filesize for usage
  end
end

1. Check status of running VMs
``` bash
vagrant status
```
2. Spin up VMs from VagrantFile
```
vagrant up
```
3. Login to one of the machines 
```
vagrant ssh <hostname>
```
