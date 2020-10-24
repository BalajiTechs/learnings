Configuring Key Based Login
In below example, We want demouser to be able to login into machine1 from machine0 without password. Here are the steps
1. Login to machine0 
2. Login as demouser
    $su demouser 
3. Create ssh keys if not created yet. This will create key-pairs(public and private)
    $ ssh-keygen -t rsa 
4. Copy public key to machine1
    $ ssh-copy-id -i ~/.ssh/id_rsa.pub demouser@machine1
5. Try login with demouser on machine1. Below command should work without any password
    $ ssh demouser@machine1


Note: If you want to enable some other user(say demouser1) to login with ssh keys from different user(say demouser2) than do following
1. follow steps 1 to 3 considering demouser1
2. Copy public key of demouser1 to demouser2 on machine1
    $ ssh-copy-id -i ~/.ssh/id_rsa.pub demouser2@machine1
3. exeucte step 5 with demouser1    


Cases when step 5 asks password
1. Key pair was already present in ~/.ssh/ folder. In this case try to pass  -i ~/.ssh/<publickey filename> to ssh-copy-id
2. Manually generated .ssh folder. ssh is very sensitive to permission. If not generated manually permission error might occur. 
Make sure that authorized_keys ha 0600 permission.
On machine1, execute below command
    $ chmod 0600 ~/.ssh/authorized_keys


