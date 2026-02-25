- we scan the network for all the assets we may reach in which all of this assets may have vulnerabilities that we can exploit.
* ---> scanning steps are :
	1. network sweeping
	2. network tracing
	3. port scanning
	4. os fingerprinting
	5. version scanning
	6. vulnerability scanning 

- in network scanning it is best to use the ip addresses instead of the domain names 
- another tip is when scanning we use the most famous 1000 port instead of them all , or use multiple devices to scan for all the ports  to achieve  threading 
- use sniffers is a best practice that helps a lot 
------------------------------------------------
## Sniffers:
- one the most used sniffers is the **tcp dump**  it is a the base for Wireshark and is just a cli and Wireshark is GUI.
- the usage of tcp dump is as following `tcpdump -i (network name)` this the basic usage of this tool which provides simple info about the network and the tcp connection 
- a method of improving it's usage if to add `-nn` to the command to be as ` tcpdump -nn -i (network name)` this will display the ip of the server instead of it's name 
- adding the `-X` this will display the connection as hexadecimal this will be helpful , as in the forensics field it can be injected with a payload inside of this and by displaying it the payload will be discovered so the full payload will be as following `tcpdump -nn -X -i (network name)` .
- by adding `s0` to the command this will display the full request without any shortening or shortcuts 
- another method of filtering is to use filters in tcp dump as following `tcpsump -nn -X -i (network name) (tcp,udp,icmp,arp,ip) (and,or,not) (port needed) (and,or,not) (dst,src,host) s0` we can choose any of the optional commands based on what we need to filter for .
- to save the output from the commands we just made we can use the command `-w` where it is write and for the file type it must be **pcapng** , and to read the file to make analysis we use `tcpdump -r filename.pcapng`  
---------------------------------------------------
## Network sweeping :
- nmap is the best tool for this it is used from network sweeping
- first tip using nmap is to use `-sn` which scans the network using ping not port scanning , we also can make the scan into a range of ip addresses not just a single one as the following `nmap -sn (ip address).0-255` this will result in displaying all the network ip available for this domain 
- second tip is using `-sl` that lists the ip addresses while enumerating.
**---> we cant use httpx instead of nmap as httpx works on web ports so if there is an active port that is not using  a web server it will not be show **
- second tip is using `-pn` which disables host discovery and treats all port as they are live and working and proceed  to port scanning directly 
- third tip is to use `-sS`to scans for tcp syn scan without listening 
**---> so we can use nmap as following `nmap -n -sn -sS -Pn (target ip) `** 
-------------------------------------------------------
## Network tracing :
- to trace the network and its packets we use tracroute tool. which tracks the packet from the router al the way to the destination server 
- we use trace route as following `tracroute -n (target ip)`this will be using udp for the trace and most likely will get blocked so it is the worst possible method
- another method to be used which is using icmp as following `tracroute -l (target ip)`
- for tcp tracing it is as following `traceroute -t (trget ip)`
--------------------------------------
## port scanning :
- we start by using nmap as following `nmap -pn -T 3 (ip addrress)`, the (-T) stands for time , is done to make more time to prevent any detection by load balancer or  the ips.
- 


