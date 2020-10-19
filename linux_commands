---------------------------------------------------------------------------------------------------
networking commands
1. To see netowrk routing for ping and ssh 
mtr - network diagnostic tool

2. Setting up network in multiuser installation of centos 7
    a. Type “nmcli d” command in your terminal for quick list ethernet card installed on your machine:
    b. Type “nmtui” command in your terminal to open Network manager. After opening Network manager chose “Edit connection” and press Enter (Use TAB button for choosing options).

3. Command for minimal setup of centos 7        
    $ ip n 
    $ ip addr
    $ ip r ( to see route details)
    $ yum install net-tools( to install netstat)
    http://www.tecmint.com/things-to-do-after-minimal-rhel-centos-7-installation/5/

4. ADD Route to 10.208.22.14
    $ ip route add 10.208.22.1 dev eno16777728

5. See open ports on linux without netstat
    $ lsof -i | grep 9830
    $ cat /etc/services | grep 834
    $ nmap -sT -O localhost

6. Get list of all tcp connection
    $ lsof -i TCP
7. Get list of all tcp connection to remote 8080 port
    $ lsof -i TCP:8080

8. Network interface issue on ubuntu
    Sympotms
        1. `ifconfig` doesn't show any iterface other than lo
        2. `ip addr` shows eth interface but it is down
        3. `ifup eth0` shown the interface does not exists
        4. `ifconfig -a` shows an interface that is down
    Solution: the issue may have occured because interface name changed. This can occur when you move your machine from one cloud to other cloud-init
    check "/etc/network/interfaces" file and update the name of interface as shown in `ip addr` command    
---------------------------------------------------------------------------------------------------
grep commands

1. Searcing for a word in all file( use -ril option to list file name only)
    $ grep -ri  <word> *
2. 

---------------------------------------------------------------------------------------------------
find commands

1. Find all files starting with message
    $ find -iname  "message*"
2. Find all directory in current folder where the commnad is fired
    $ find -type d 
3. Find files older than x days(only look in specified folder as depth is 1)
	$ find /tmp/ -maxdepth 1 -type f -mtime +x 
4. Find folder older that x days
	$ find /tmp/ -maxdepth 1 -type d -mtime +x 

5. Delete all files older than x days
	$ find /tmp/ -maxdepth 1 -type f -mtime +x -delete
6. Find all java files and copy to some directory
    $ find .  -iname "*.java" -type f  -newer start_date -exec cp {} /tmp/cid \;
7. Find all lines in one file that are present in another file
    $ for i in `cat ../../../../junit_test_result/tests.pending.txt`; do  grep -r $i skipped.txt ; done
8. Find all result.log file  in current directory(recusrively) and follow links
    find -L . -type f -iname "result.log"

---------------------------------------------------------------------------------------------------
systemctl commands

1. To start centos in server mode (command line only) execute below command as root user
    $ systemctl set-default multi-user.target
2. Setting hostname on systemd linux env
 hostnamectl set-hostname <hostname>

---------------------------------------------------------------------------------------------------
firewalld commands

1. Add IP ranges in trusted zone
    $ firewall-cmd --add-source=192.168.9.1/24 --zone=trusted;firewall-cmd --reload
2. Change the zone of IPs if already present in a zone
    $ firewall-cmd --change-source=192.168.9.0/24 --zone=public;firewall-cmd --reload
    $ firewall-cmd --add-port=8080/tcp --permanent;firewall-cmd --reload    

---------------------------------------------------------------------------------------------------
Other userfull commands
1. Find out if the process running( all users)
    $ ps aux | grep -i resourcemanager
2. Creating SUDO user on centos/redhat/fedora
    $ adduser exampleuser -g wheel
3. List entries in keystore file
    $ keytool -list -v -keystore keystorefile.jks    
4. Download java using wget 
    $wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.rpm
5.  Download package and its dependecies 
    $ yum install gparted-0.19.1-6.el7.x86_64.rpm --downloadonly --downloaddir=./  //
6. Check no of threads active 
    top -b -H -u root -n 1 | wc -l
7. Remove password from certificate key
openssl rsa -in /root/all_certs/private/cakey.pem -out /root/all_certs/private/cakey_no_pass.pem

---------------------------------------------------------------------------------------------------
disk/partition related commands
1. Extending root partition by reducing home partition size
    a. Backup the contents of /home
        $ tar -czvf /root/home.tgz -C /home .
    b. Test that backup is fine
        $ tar -tvf /root/home.tgz
    c. Unmount home
        $ umount /dev/mapper/centos-home
    d. Remove the home logical volume
        $ lvremove /dev/mapper/centos-home
    e. Recreate a new 400GB logical volume for /home, format and mount it
        $ lvcreate -L 400GB -n home centos
        $ mkfs.xfs /dev/centos/home
        $ mount /dev/mapper/centos-home
    f. extend your /root volume with ALL of the remaining space and resize (-r) the file system while doing so
        $ lvextend -r -l +100%FREE /dev/mapper/centos-root
    g. restore your backup
        $ tar -xzvf /root/home.tgz -C /home
    h. check /etc/fstab for any mapping of /home volume. IF it is using UUID you should update the UUID portion. (Since we created a new volume, UUID has changed)
    
 
2. Clean root space 
    a. Remove tmp files in /tmp folder
    b. Remove old kernel rpms
	  	$ package-cleanup --oldkernels --count=1
    c. Move /home directory to other storage
    d. Clean /var/log/messages
    e. Clean core files
    f. yum clean all
    g. Find top 10 large files
        $ du -sk * | sort -nr | head -10
        $ du -sh /*
    h. Clean mysql binlogs. If /var/lib/mysql consuming considerable space then you need to clean some mysql space
	    $ du -sk /var/lib/mysql | sort -nr | head -10
        Check  if binlog files are consuming space in /var/lib/mysql folder. If Yes then execute below command to purge logs older than 3 days. Attention Only execute below command if you are not using replication (see  http://www.cyberciti.biz/faq/what-is-mysql-binary-log/ site for more information)
        $ mysql -u root -p 'MyPassword' -e "PURGE BINARY LOGS BEFORE '2008-12-15 10:06:06';"
 
3. https://rbgeek.wordpress.com/2013/01/27/how-to-extend-the-root-partition-in-lvm/
  xfs_growfs  /dev/centos/root

4. Moving home partition
    https://help.ubuntu.com/community/Partitioning/Home/Moving
    a. Find the uuid of the Partition. First mount empty partition(on which home will be mounted)
        sudo blkid
    b. Setup Fstab
        $ sudo cp /etc/fstab /etc/fstab.$(date +%Y-%m-%d)
        $ cmp /etc/fstab /etc/fstab.$(date +%Y-%m-%d)
        $ sudo gedit /etc/fstab 
    and add these lines into it 
        # (identifier)  (location, eg sda5)   (format, eg ext3 or ext4)      (some settings) 
        UUID=<uid obtained from blkid>  /media/home    ext3          defaults       0       2 
        sudo mkdir /media/home
        sudo mount -a
    c. Copy /home to the New Partition
        sudo rsync -aXS --exclude='/*/.gvfs' /home/. /media/home/.
    d. Check Copying Worked
        sudo diff -r /home /media/home -x ".gvfs/*"
    e. Preparing fstab for the switch
        sudo gedit /etc/fstab
    and now edit the lines you added earlier, changing the "/media/home" part to simply say "/home" so that it looks like this:
        # (identifier)  (location, eg sda5)   (format, eg ext3 or ext4)      (some settings) 
        UUID=????????   /home    ext3          defaults       0       2
    f. Moving /home into /old_home
        cd / && sudo mv /home /old_home && sudo mkdir /home
    g. Reboot or Remount all
        sudo mount -a

    Note: If you receive an error like 'The volume may already be mounted', use the following command to unmount the drive first before re-doing the last step again. (note the "n" should be missing from the command, making it "umount")
	    sudo umount /media/home/
    Then try mounting again
	    sudo mount -a
    Deleting the old Home
	    cd /
	    sudo rm -rI /old_home 

5. To create a new partition on Linux
    Start fdisk 
    /sbin/fdisk /dev/sdb

    where /dev/sdb stands for the drive that you want to partition.
    In fdisk, to create a new partition, type the following command:

    $ n
        When prompted to specify the Partition type, type p to create a primary partition or e to create an extended one. There may be up to four primary partitions. If you want to create more than four partitions, make the last partition extended, and it will be a container for other logical partitions.
        When prompted for the Number, in most cases, type 3 because a typical Linux virtual machine has two partitions by default.
        When prompted for the Start cylinder, type a starting cylinder number or press Return to use the first cylinder available.
        When prompted for the Last cylinder, press Return to allocate all the available space or specify the size of a new partition in cylinders if you do not want to use all the available space.
    By default, fdisk creates a partition with a System ID of 83. If you're unsure of the partition's System ID, Enter below command to check it.
    $ l
    Use elow command to write the changes to the partition table.
    $ w
    /sbin/mkfs -t ext3 /dev/hda3
    Create a directory that will be a mount point for the new partition. For example, to name it data, enter:
    mkdir /data

    Mount the new partition to the directory you have just created by using the following command:
    mount /dev/hda3 /data

    Make changes in your static file system information by editing the /etc/fstab file in any of the available text editors. For example, add the following string to this file:
    /dev/hda3 /data ext3 defaults 0 0

    In this string /dev/hda3 is the partition you have just created, /data is a mount point for the new partition, Ext3 is the file type of the new partition. For the exact meaning of other items in this string, consult the Linux documentation for the mount and fstab commands.
    Save the /etc/fstab file.
			
6. Logical Volume Manager(LVM) - Steps to create lv, pv, vg

    a. create a partition(use fdisk /dev/<disk> -----> n ---> p ---> enter --->enter --> w  ---- Done). This will create a disk partition(fdisk -l to check partition created) for e.g. /dev/sda1 .
    b. Create Physical Volume(PV) --> pvcreate /dev/<disk Partition>
    c. Create Volume Group(VG) ---> vgcreate <volume group name> /dev/<disk partition1> /dev/<disk partition2> ....
    d. Create Logical Volume in above VG ---> lvcreate -n <name of logical volume>  -L <size> <volume group name> (for e.g. lvcreate -n hadoop_lv -l 100%FREE example_vg)
    e. Format the new volume --> mkfs.ext4 /dev/<vg name>/<lv name>
    f. Mount the LV -> mount /dev/<vg name>/<lv name> /path/to/mount/
Note: While extending the logical volume do 'resize2fs /dev/<vg>/<lv>' to gain the extended space.
7. Extending the partition
    $ fdisk -l
    $ fdisk /dev/sda
    $ df -h
    $ fdisk -l
    $ df -h
    $ pvs
    $ pvcreate /dev/sda2
    $ vgextend /dev/example_vg /dev/sda2
    $ lvextend /dev/example_vg/hadoop_lv /dev/sda2
    $ df -h
    $ resize2fs /dev/example_vg/hadoop_lv
    $ df -h
    $ vgs
    $ lvextend /dev/example_vg/hadoop_lv /dev/sda1
    $ resize2fs /dev/example_vg/hadoop_lv
8. Extending root(centos-root) volume
    $ fdisk /dev/sdb
    $ pvcreate /dev/sdb1
    $ vgextend /dev/centos /dev/sdb1
    $ lvextend /dev/centos/root /dev/sdb1
    $ xfs_growfs /dev/centos/root (or try xfs_growfs /)
    $ df -h

9. Add SWAP from lvm. To add a swap volume group (assuming /dev/VolGroup00/LogVol02 is the swap volume you want to add):
    a. Create the LVM2 logical volume of size 256 MB:
        $ lvm lvcreate VolGroup00 -n LogVol02 -L 256M
    b. Format the new swap space:
        $ mkswap /dev/VolGroup00/LogVol02
    c. Add the following entry to the /etc/fstab file:
        $ echo "/dev/VolGroup00/LogVol02   swap     swap    defaults     0 0" >> /etc/fstab
    d. Enable the extended logical volume:
        $ swapon -va
    e. Test that the logical volume has been extended properly:
        $ cat /proc/swaps
        $ free
10. Adding disk without reboot linux(SCSI only)
	$ df -ih
	$ ls
	$ jps
	$ ls /sys/class/scsi_device/
	$ echo 1 > /sys/class/scsi_device/0\:0\:0\:0/device/rescan
	$ fdisk -l
	$ ls /sys/class/scsi_device/
	$ echo 1 > /sys/class/scsi_device/2\:0\:0\:0/device/rescan
	$ fdisk -l
	$ fdisk /dev/sda
	$ fdisk
	$ fdisk -l
	$ partprobe
	$ pvcreate /dev/sda2
	$ vgs
	$ vgextend /dev/sda2
	$ vgextend hadoop_vg /dev/sda2
	$ lvextend hadoop_lv /dev/sda2
	$ lvextend /dev/hadoop_vg/hadoop_lv /dev/sda2
	$ lvs
	$ vgs
	$ pvs
	$ resize2fs /dev/hadoop_vg/hadoop_lv

11. Mount a partition readwrite
    $ mount -o remount, rw /dev/sd
    

12. Create /home Partition manually
Pre-Requisite/Assumption -> you have space left in centos volume group or there is some other physicial volume that you can use to create HOME volume. 

    Assuming that centos volume group(vgs will show the remaining space) have 8GB of free space
    1. lvcreate /dev/centos/home -L 8G
    2. mkfs-ext4 /dev/centos/home
    3. add entry in /etc/fstab as below
    /dev/mapper/centos-home /home                   ext4     defaults        0 0
    4. execute "mount -a"
    5. If using SELinux policy, Execute below command to label the /home correctly
    restorecon -R -v /home    



-------------------------------------------------------------------------------
Analysing disk space issue with ncdu
go to folder that you want to analyse and run ncdu command(install it if not present.)

-------------------------------------------------------------------------------

Install VNC server 
Below are the steps to enable vnc-server. These steps need to be perfomed in GUI mode
yum install tigervnc-server
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service

edit vncserver@:1.service file
vi /etc/systemd/system/vncserver@:1.service

Replace the string <USER> with appropriate vncuser’s username. 
firewall-cmd --permanent --zone=public --add-service vnc-server; firewall-cmd --reload

su - <USER>
vncserver

Now make the service enabled on after every reboot with root credentials:
su -
systemctl daemon-reload
systemctl enable vncserver@:1.service
reboot
systemctl start vncserver@:1.service

Source : https://www.howtoforge.com/vnc-server-installation-on-centos-7


Connecting VNC from terminal
	ssh using your credentials
	execute vncserver command
	supply passwd if asked(this password will be used in vncclient also)
	note down the vnc server id (e.g. myhostname:6)
	open vnc client on windows(ultravnc) and enter the ID and connect 
==============================================================================
--------------------------------------------------------------------------------------------------
Start java in debug mode 
java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=5005 -jar <jar name>
--------------------------------------------------------------------------------------------------
To indent xmlfile on linux
xmllint --format --recover foo.xml

--------------------------------------------------------------------------------------------------
Search for all MIME files accuring filedescriptor
    $ ls -lart /proc/51985/fd/ |grep MIME| awk '{print $9}' > 1

--------------------------------------------------------------------------------------------------
Changing BASH shell tag
export PS1="[\u@localhost \W]\$ "
--------------------------------------------------------------------------------------------------
Time Synchronization in Linux
ntpdate comes preinstalled as ntp client. add your ntp server name in /etc/ntp/
1. using NTP
    command to see if ntp is synchronized
		ntpstat
	Command to see which server are configure as ntp server 
		ntpq -p
	See if NTPD is running
		systemctl status ntpd.service
		
2. Using chronyd
	Checking chrony Tracking
		chronyc tracking
	Checking chrony Sources
		chronyc sources
		note: ^ means ntp server and ? mean not connecting (^* mean connected and synched)
	 
		chronyc sourcestats
		
Sources: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-Checking_the_Status_of_NTP.html
		https://docs.fedoraproject.org/en-US/Fedora/18/html/System_Administrators_Guide/sect-Checking_if_chrony_is_synchronized.html

--------------------------------------------------------------------------------------------------
screen command
Help 
	ctrl+a ?
Detach a screen and go back to real console.
	“Ctrl-A” and “d“
Re-attach the screen: execute below command on shell 
	screen -r
If mulpiple deatched screens are runiing then check ID and execute below command
	screen -r <id>
Create a screen with given name and enable window logging
    screen -s -L remove_orphan_files
Using Multiple Screen
    “Ctrl-A” and “c“    -----> create new screen
    “Ctrl-A” and “n“	-----> Next Screen
    “Ctrl-A” and “p“	-----> Previous Screen
    “Ctrl-A” and  " 	-----> All screen window
Lock Screen
    ctrl+a and x
“Ctrl-A” and “K” to kill the screen.

--------------------------------------------------------------------------------------------------
Find all java process on all servers(consucutive IPs)
for i in {1..3}; do ssh 192.168.8.15$i "hostname;jps;echo -e '\n'";done

#Execute a command on multiple hosts sequentially
for i in {node1,node2,node3}; do ssh $i "hostname ";done
for i in {1..3}; do ssh hadoop-node$i "echo "Hostname : `hostname`";zkServer.sh start;echo -e '\n'";done

--------------------------------------------------------------------------------------------------
Too many open files problem
a. check limit using below command
	$ uname -a

b. for Dynamically changing the limit 
	$ ulimit -n 8192
	The updated value can then be printed
	$ ulimit -n
    Check with uname -a
c. For permanent setting, as root edit /etc/security/limits.conf
		and add a line such as
		*               soft    nofile            8192

--------------------------------------------------------------------------------------------------
Copy all images to external hard-drive
	$ ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory

Search all jpg images in the system and archive it.
	$ find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz

--------------------------------------------------------------------------------------------------
Clean old kernels
package-cleanup --oldkernels --count=1

--------------------------------------------------------------------------------------------------
Reading a file line with spaces in filename
If you don't supply an argument to the "read" call, read will set a default variable called $REPLY which will preserve whitespace. 
So you can just do this
$ cat test.file | while read; do echo "$REPLY"; done

--------------------------------------------------------------------------------------------------
Searching for jars than contains class
 find . -name "*.jar" | xargs grep "org.omg.ETF.Connection"

--------------------------------------------------------------------------------------------------
Issue : Can't locate Archive/Extract.pm in @INC (you may need to install the Archive::Extract module)
Solution :  Centos 
				sudo yum install "perl(Archive::Zip)"
			Windows
				PATH=/c/StrawberryPerl/perl/bin:/c/StrawberryPerl/c/bin:$PATH
				export PATH

--------------------------------------------------------------------------------------------------
Installing PIDGIN on centos 7
rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro 
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm
yum repolist
yum install pidgin
yum install pidgin-sipe

--------------------------------------------------------------------------------------------------
Installing Eclipse on Centos
    Switch to root
        $ su
    Install JDK
        $ yum -y install java-1.8.0-openjdk
    Download eclipse-oxygen
        $ curl -O http://ftp.jaist.ac.jp/pub/eclipse/technology/epp/downloads/release/oxygen/1a/eclipse-java-oxygen-1a-linux-gtk-x86_64.tar.gz

    Extract
        $ tar -zxvf eclipse-java-oxygen-1a-linux-gtk-x86_64.tar.gz -C /opt
    Create link
        $ ln -s /opt/eclipse/eclipse /usr/bin/eclipse

    Create App Menu entry: Create file and paste given content
        Filename:  "/usr/share/applications/eclipse-4.7.desktop"
        Content : 
            [Desktop Entry]
            Encoding=UTF-8
            Name=Eclipse 4.7
            Comment=Eclipse Oxygen
            Exec=/usr/bin/eclipse
            Icon=/opt/eclipse/icon.xpm
            Categories=Application;Development;Java;IDE
            Version=1.0
            Type=Application
            Terminal=0

    Start from Command Line
        $ eclipse
    Start From App Launcher
        On Gnome 3, Application >> Programming >> Eclipse.

--------------------------------------------------------------------------------------------------
reposync -c /etc/yum/yum.conf -n -d -g comps.xml --download-metadata --norepopath -r openSUSE_Leap_15.0_Update --download_path=/data/repo/zypper

--------------------------------------------------------------------------------------------------
search for a string in all build.xml file
    grep -ri instrument **/*/build.xml

--------------------------------------------------------------------------------------------------
Install VLC on centos
yum -y install http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
yum install vlc    

--------------------------------------------------------------------------------------------------
See what all users doing on linux
$ w

--------------------------------------------------------------------------------------------------
Change TimeZone on linux centos
$ tzselect 
Select required timezone from options
Follow instruction to change timezone permanently

--------------------------------------------------------------------------------------------------
Setting size of gnome desktop icons(centos 7)    
    $ gsettings set org.gnome.nautilus.icon-view default-zoom-level small

--------------------------------------------------------------------------------------------------
Disable cloud-config at startup(AWS)
#cloud-config
bootcmd:
    - echo 'APT::Periodic::Enable "0";' > /etc/apt/apt.conf.d/10cloudinit-disable
    - apt-get -y purge update-notifier-common ubuntu-release-upgrader-core landscape-common unattended-upgrades

--------------------------------------------------------------------------------------------------
Check your initiator name
vi /etc/iscsi/initiatorname.iscsi

Check existing connections
iscsiadm -m session

Discover targets
iscsiadm -m discovery -t st -p 192.168.12.20

Login 
iscsiadm -m node -T iqn.2016-02.local.itzgeek.server:disk1 -p 192.168.12.20 -l

Logout
iscsiadm -m node -T iqn.2016-02.local.itzgeek.server:disk1 -p 192.168.12.20 -u

--------------------------------------------------------------------------------------------------
Download a package without wget 
curl http://mirror.centos.org/centos/7/os/x86_64/Packages/telnet-0.17-64.el7.x86_64.rpm > telnet.rpm

--------------------------------------------------------------------------------------------------
Check crons running as cron.daily  tasks
run-parts --test /etc/cron.daily

--------------------------------------------------------------------------------------------------
apt-get cheatcode
1. Check available version of software for downgrade purpose
    $ sudo apt-cache showpkg vim

2. install specific version of VIM(2:7.4.1689-3ubuntu1) including dependecies
    $ sudo apt-get install vim=2:7.4.1689-3ubuntu1 vim-common=2:7.4.1689-3ubuntu1 vim-runtime=2:7.4.1689-3ubuntu1

--------------------------------------------------------------------------------------------------
Zypper Cheat Sheet

1. Listing Needed Patches
    $ zypper list-patches or zypper lp

2. Applying Patches
    $ zypper patch

3. Checking Patches
    $ zypper patch-check or zypper pchk

4. Listing All Patches
    $ zypper patches

5. Getting Information About Patches
    $ zypper patch-info
    $ zypper info -t patch

6. Packages Updates
    $ zypper list-updates or zypper lu
    $ zypper update or zypper up

7. Downgrade a package in suse
https://stackoverflow.com/questions/25995813/zypper-update-package-to-the-previous-version-not-the-last

    $ zypper pa -ir SLE-Module-Public-Cloud12-Updates
    $ zypper info cloud-init
    $ zypper in cloud-init=17.1-37.9.6
    $ zypper in --oldpackage cloud-init=17.1-37.9.6
    $ zypper patch-info package:cloud-init
    $ zypper list-patches

--------------------------------------------------------------------------------------------------
YUM command cheatcode
Get status of updates with severty levels
    yum updateinfo summary

To upgrade packages that have security errata
    yum --security update

To show a list of all BZs that are fixed for packages you have installed
    yum updateinfo list bugzillas

To check updates only
    yum check-update

--------------------------------------------------------------------------------------------------
Linux renew ip command
dhclient -r  //release the current lease
dhclient     //get the new IPs

--------------------------------------------------------------------------------------------------
disable selinux temoprarity
setenforce 0


--------------------------------------------------------------------------------------------------
Nginx Setup
    yum install epel-release
    yum install nginx
    cd /etc/nginx/
    vim nginx.conf
    mkdir /etc/ssl/private
    chmod 700 /etc/ssl/private
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
    openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
    vim nginx.conf
    systemctl restart nginx
    vim /opt/C-DAC/jetty9.1.0.M0/example-jetty.xml
    systemctl restart nginx
    systemctl restart example_viewer
    systemctl restart nginx

On system from where/ to where you connect to this nginx peer, copy nginx-selfsigned.crt in $JAVA_HOME/jre/lib/security and add to trusted cacerts using below command
    keytool -import -alias nginxca -keystore cacerts -file nginx-selfsigned.crt

Check if a module is installed in nginx 
    2>&1 nginx -V | tr -- - '\n' | grep _module

--------------------------------------------------------------------------------------------------
Disable IPv6 using sysctl settings (no reboot required)
To verify if IPv6 is enabled or not, execute :
	# ifconfig -a | grep inet6
	
Append below lines in /etc/sysctl.conf:
	net.ipv6.conf.all.disable_ipv6 = 1
	net.ipv6.conf.default.disable_ipv6 = 1
	
To make the settings affective, execute :
	sysctl -p

--------------------------------------------------------------------------------------------------
rsynv folder with exculed
rsync -av myfolder --exclude 'myfolder/exclude*' destinationhost:/path/to/destination/folder

--------------------------------------------------------------------------------------------------
Replace all "home/example" to "home/exampleuser" in file exampleclient.properties
 sed -i 's/home\/example\//home\/exampleuser\//g' config.ini

--------------------------------------------------------------------------------------------------
Testing Slowloris attack
Install slowhttptest
	yum install slowhttptest
Execute the command against the server(4000 connections)	
	slowhttptest -c 4000 -H -g -o apache_no_mitigation -i 10 -r 200 -t GET -u https://example.com -x 24 -p 3 -l 120

--------------------------------------------------------------------------------------------------
Upgrading from centos 7.3 to 7.4 with epel enabled
Step 1. Try "yum update". 
Fix 1.  If fails due to libgpod then first do "yum downgrade libgpod" then do "yum update"
Fix 2. If failing due to 'ipa' then do "yum remove freeipa" then do "yum update"

--------------------------------------------------------------------------------------------------
CPU Details on centos
cat /proc/cpuinfo
lscpu

--------------------------------------------------------------------------------------------------
add user to a group in linux
usermod -u example -g wheel

--------------------------------------------------------------------------------------------------
install pip on linux
    $ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    $ python get-pip.py

install jinja2
    $ pip install jinja2    