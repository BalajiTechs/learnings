Mysql Tricks
1. To access remote mysql db on a Machine open mysql console with admin and execute below command. 
    $ grant all privileges on *.* to root@'192.168.8.0/255.255.255.0' identified by '<groupPass>';

2. Grant MySQL user permission access from outside IP
    $ mysql -u root -p
    Enter password: #put your password here
    mysql> grant all on *.* to 'root'@'%' IDENTIFIED BY 'securepassword';
    
    Note: If above do not work then use this 
    "GRANT ALL PRIVILEGES ON logicaldoc.* TO 'logicaldoc'@'10.208.21.0/255.255.255.0' IDENTIFIED BY 'securepassword' with grant option;"
    Also use hostname as login

    And then Open port 3306
        firewall-cmd --add-port=3306/tcp --permanent;firewall-cmd --reload
    Access the DB using heidiSQL with username = root password =securepassword
	
3. Clearing Binary files
The binary log contains all statements that update data or potentially could have updated it. To clear these binary log files execute below command
    $ mysql -u root -p 'MyPassword' -e "PURGE BINARY LOGS BEFORE '2008-12-15 10:06:06';"

Also check http://www.cyberciti.biz/faq/what-is-mysql-binary-log/ site for more information

4. JOIN of table oid and commonmetadata to get all OID sorted by date(recievedat)
    $ select b.objectid from index.commonmetadata a, exampleindex.oid b  where a.recordid=b.recordid order by a.recievedat
