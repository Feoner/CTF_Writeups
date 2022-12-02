# Nycon
This root to boot involes exploting an Sql Injection vulnerability when updating your chart. Privelage escalation 
is achieved by triggering a double free on the route4_filer object. 

## NMAP
<p align="center">
<img src="CTF_Writeups/resources/nmap.png">
<br>
  After crawling the website we notice that if we add an item to our cart the script update-cart.php is called. Here the id= parameter will accept arbitrary input. 
  
 
