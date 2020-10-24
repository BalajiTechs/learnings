Check status of local files from repo
    svn status -u


Adding new file/folder to svn
    mkdir <folder>
    cp <file> <folder>
    svn add <folder>
    svn add <folder>/<file>
    svn commit -m <message>

==============================================================================================
To get RabbitVCS under Thunar working in CentOS 7 x86_64

--------------------
Open terminal as root user and run following commands:

1. yum install thunar gtk-doc Thunar-devel
2. yum install meld pysvn python-dulwich python-simplejson subversion
3. rpm -ivh rabbitvcs-core-0.14.2.1-5.el7.centos.noarch.rpm rabbitvcs-cli-0.14.2.1-5.el7.centos.noarch.rpm thunarx-python-0.2.3-5.el7.centos.x86_64.rpm rabbitvcs-thunar-0.14.2.1-5.el7.centos.x86_64.rpm
--------------------
Updated steps for support of nautilus
1. rpm -e rabbitvcs-core rabbitvcs-cli thunarx-python rabbitvcs-thunar
2. cd Updated-for-nautilus
3. yum install *.rpm
4. Restart the system and check context menu for support   
