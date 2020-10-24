#### Pre-Setup
You need an ip to set up ldap admin server so follow below steps
add entry in /etc/hosts providing your IP and FQDN. 
> If FQDN not available then you can put hostname.localdomain  against IP
	
#### Installation and setup
- To install 389-DS 
``` bash
yum install epel-release
yum install 389-ds
```

- Running dirsrv and ds-admin  at startup
``` bash
systemctl enable dirsrv-admin.service
systemctl enable dirsrv.target
systemctl start dirsrv@localhost.service
systemctl restart dirsrv-admin
```

- Remove 389-ds completely
``` bash
remove-ds-admin.pl -y -f
yum remove 389-ds-base-libs 389-adminutil idm-console-framework -y   
rm -rf /etc/dirsrv /usr/lib*/dirsrv /var/*/dirsrv /etc/sysconfig/dirsrv*
```    

#### Tips
> if SELinux creating problem for a port execute below command to see if the port is present in allowed list
``` semanage port -l | grep 9830 ```
>
> While connecting to Windows 389-ds client when only IP is known then add the FQDN and IP set in **C:/Windows/system32/driver/etc/hosts**
Doing above will let you connect to the 389-ds server where domain name server is not present

#### Test using LDAP commands
1. Adding a new user 
    1. Create ldif as shown below(newUser.ldif)
        ```
        dn: uid=sitapaliwal@example.in,ou=site,ou=example,ou=People,dc=site,dc=example,dc=in
        objectClass: top
        objectClass: person
        objectClass: organizationalPerson
        objectClass: inetorgperson
        givenName: sita
        cn: sitaPaliwal
        sn: paliwal
        title: strongest mom of the world
        mail: sitapaliwal@example.in
        uid: sitapaliwal@example.in
       ```
    2. execute below command
        ```
        $ ldapadd -d 7 -x -D "cn=Directory Manager" -W  -h localhost -f newUser.ldif
       ```

2. Add userpassword as below
    ```
    $ ldapmodify -d 7 -D "cn=Directory Manager" -W -h localhost -f mod.ldif
    ```

    Content of mod.ldif file
    ```
    dn: uid=sitapaliwal@example.in,ou=site,ou=example,ou=People,dc=site,dc=example,dc=in
    changetype: modify
    add: userPassword
    userPassword: sitapaliwal
   ```
	> To change the password use replace: userPassword

3. Search all entries in ldap
    ```
   $ ldapsearch -x -h localhost -b "dc=cloud,dc=domain,dc=in"
   ```