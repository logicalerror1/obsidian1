- google dorking is a recon method used to gather info that is public for a small target that may have some info that is leaked or misconfigured 
- we start searching info as following `site: *.google.com`, this will gather everything .google.com
---> some dorks of getting more email addresses are :
 1. site:Domain.com "@example.com"
 2. intext:"email" OR "contact" site:example.com
 3. filetype:xls OR filetype:csv "@example.com"

- ssl for Shodan dorking all of the output will be websites with no firewall or any protection this will also give us the original ip address of the website with no protection layers added

- ==exploit db provides a variety of dorks that is updated regularly== this is most useful if searching for information disclosure. 
  