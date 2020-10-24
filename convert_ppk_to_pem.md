Step 1 – First of all, install the putty tools on your Linux system using below command.
$ sudo apt-get install putty-tools
Step 2 – Now, convert the ppk file to pem file using puttygen command line tool.
$ puttygen server1.ppk -O private-openssh -o server1.pem
Step 3 – Change the .pem file permissions. Set the read-only permissions to the owner of the file, remove any permission to group and other. Other wise ssh will refuse this key for use.
$ chmod 400 server1.pem
Step 4 – Finally, connect to your remote Linux server with ssh using this pem key.
$ ssh -i server1.pem ubuntu@11.22.33.44
