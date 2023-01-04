# Precious
This is a linux mahcine on Hack the Box rated easy. The intial foothold comes from injecting commands into a web page to PDF convertor. Privelage escalation relvoves around exploiting an RCE vulnerablitiy in a dependency.yaml file.

## NMAP


## SQL Injection
Navigating to the webpage we find a webpage to PDF convetor. Searching online these types of software are pretty common so to narrow down our search we need to find the specific version and software that this one is running on. If we run a simple http server with python we can test giving it different pages to convert. If we inspect elements of the pdfs that are spit out we are able to determine that this is running pdfkit. Pdfkit does not properly sanitize the url. If we append our python server with ?name=)'%20 we will be able to inject commands. We can test this with sleep. After confirming with sleep with can try to cat out /etc/passwd. We get a couple of users but no hashs or passwords. I initially tried to get a reverse shell with nc but that didnt work. Might be a coincidence but a clue for what we needed is the user named ruby. After injecting a ruby reverse shell into the url we are able to get a shell. 

## Lateral Movement
We get our intial shell as ruby. This user wasnt able to use sudo and after trying to enumerate the machine, I wasnt able to find any sort of possible privilege escalation paths. If we think about the way needed to get a shell, we can look at other possible ruby files. We are able to read the bundle.config file. In this file we find creds for the user henry.

## Privilege Escalation
As the user henry we are able to run one file as sudo. Looking at the script we can see that it calls dependcencies.yml. If we search for potential exploits we find an RCE vulnerability. Transfering over the poc and running the script we get a root shell.
