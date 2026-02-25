--> recon is the process of collecting assists and all what is related to the network
- osint is part of the recon process in which we can collect a lot of  valuable info such as :    
 1. ip addresses
 2. mail servers
 3. DNS servers
 4. Alias names
 5. Subdomains
 6. Emails
 7. users
 8. application 
 9. Antivirus
 10. Network Range
_______________________________________________________________
##  Mail servers :
- most used way in gathering IP addresses is  the **dig** tool :
	- in which this command is used `dig +noall +answer (domain)`
	- to get the name server of the domain we use `dig +noall +answer (domain) NS`
	-  to get the ipv4 its `dig +noall +answer (domain) A`
	- for the ipv6 its `dig +noall +answer (domain) AAAA`
	- , for the alias name is `dig +noall +answer (domain) CNAME`
	- and for the mail server is `dig +noall +answer (domain) MX`
  if the result of dig is too short make sure to change the DNS IP that tool asks first it exists in `etc/resolve.conf` 
- a misconfiguration on the servers might be the *zone transferee* where if u ask the server it will reply with all the info about it this is done using `dig +noall +answer @(mail server) (domain.com) axfr` **this will also provide all the subdomains and all the info about the target** it is also automated by dig as `dif +noall +answer -d (domain) -t AXFR `
 
- another tool that is widely used is **DNS recon** tool :
  - it is used as following `dnsrecon -d (domain)`, in which it collect and specialize in DNS servers
  - another way of getting more info is to specify a certain mail server as  following `dnsrecon -d (domain) -n 8.8.8.8` 
  - another method of gathering info about a  target is using brute force using dnsrecon as following `dnsrecon -t brt -d (domain) -D file.txt`, we use brute force to get info that the tools may not be able to get or maybe the value is unsigned on the servers

________________________________________________________________

## subdomains && IP Addresses :
- we collect subdomains in network as we can then translate the subdomain into ip addresses then we can test the network on it for open ports or others
- we collect subdomains using the following tools :
	- sublister
	- amass
	- subfinder
	- assetfinder
	- find-domains
	- theHarvester
	- security trails
	- findsubdomains.com
	- crt.sh
	- recon-ng
	- google Dorking

1.  Using subfinder as following `subfinder -d hackerone.com` this will result in basic info about the website , to obtain better findings we can edit the API's in the (home/bull/.config/subfinder/provider-config.yaml) **NOTE : add crt.sh to the API as it is not provided in the tool**

	-  to filter most of the collected domains from duplicates and error messages we use HTTPX tool , it is used as following `cat sub.txt |httpx -mc 200` here we printed a file of subdomains that we collected and used a pipeline to run httpx on them to return only the statues code 200
	- adding more status code to the command will result in more subdomains such as 301,302,529 as there is redirect for the 300 and ratelimite for the 500 and other server errors

2. ==we can collect more info using== [[Google Dorking]] .
3. another tool for subdomain enumeration is *one for all* it gather a lot of tools in one place to gather most of subdomains we need to edit [one for all](https://github.com/shmilylty/OneForAll/blob/master/docs/en-us/README.md)  to increase this tool productivity we need to edit it's API's as well 
4. recon-ng is a powerful tool and is widely used after installing it we start it by typing its name recon-ng this will start the instance of the framework then we show every module inside  `marketplace search` , then we install the module we want using `marketplace install  (module) `, then to access the module we use `modules load (module name)` 
5. another command that can be used to translate the domain into IP address is **host** where it is used as `host (subdomain)` it will result in the IP of the subdomain 
6. leaked emails and passwords are vulnerability that can be reported and can get a bounty for it so a measure of bug bounty is to to search for leaked emails and passwords and try to access those accounts then report it with its impact
7. 
___________________________________________________

## Network Range:
-  we use whois to get the network range or we use the website (who is look up).
- another method is to use dig to get the ip , then we use dnsrecon on the ip we found  but it will require a CIDR which we don't have so we start by guessing with trail and error .
**the PTR is exactly the opposite of the DNS where we give it ip it translate it into IP**
________________________________________________________
## Applications :
- we collect the used application as it may contain vulnerability  that we can exploit 
- famous tools to gather info about the used application is :
	1. wappalyzer
	2. whatweb
	3. builtwith
	4. metagoofil (searches using google dorking)
		`metagoofil -d (domain) -t pdf,doc,docx,xls,xlxs,csv,pptx,ppt -l 100 -n10 -o metadpdf -f result.html` 
	5. metadata about the found files using  exitfool

---------------------------------------------------------
## Antivirus :
- to know the the antivirus used it can be detected using the following :
	1. headers misconfiguration (X-powered by , X-AV-detected)
	2. favicon using Shodan , and that is done by converting the favicon into hash then search this followed by antivirus as following `http favicon hash : 123456 antivirus`  hash and we might find domains that is eligible for information disclosure 
	3. cash-snoop is a module in recon-ng tool used to to detect the antivirus to the name server of the target that is cached 