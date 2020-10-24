Working with HyperV
#### Setup/Enable HyperV on windows


#### Running a VM in HyperV
>TODO

#### Accessing VM
>TODO

#### Assigning static ip to VM without disrupting internet
1. Check host ipconfig for "Default Switch". Let's assume ip address be 172.19.64.81 and netmask be 255.255.255.240
2. Go/Connect/SSH to guest(assuming ubuntu guest) and execute "sudo nmtui" command.
3. Select "Edit Connection" and press enter. Select "Wired Connection1" (assuming this is the only network connection on guest). Select "Edit" and press enter.
4. Go to IPv4 Configuration and select "Manual" from drop down.
5. Enter desired ip address in range matching host ip address and net mask(e.g. if host ip address is 172.19.64.81 and mask is 255.255.255.0 than you can use any address between 172.19.64.1 to 172.19.64.255)
6. Enter "Gateway" and "DNS Server" to ip address of host.
7. Select "OK" and press enter.
8. Select "Wired Connection1" and press enter. This will switch the connection (i.e. disconnect if connected). Press enter again to connect. * mark means connected.
9. Select <ok> and press enter
10. Select <Quit> and press enter.



