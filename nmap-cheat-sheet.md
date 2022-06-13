# NMAP Cheat Sheet

## Useful switches for nmap during reconnaissance. 

#### Port Specification Switches


Switch       | Example                | Description
--------------- | ---------------------- | ------------
-P  | nmap -p 23 192.168.1.10 | Port scanning for an specific port
-P  | nmap -p 23-100 192.168.1.10 | Port scanning for an specific range of ports 
-p  | nmap -U:110,T:443 192.168.1.10 | Scanning different port types by UDP (U) or TCP (T)
-p-  | nmap -p- 192.168.1.10 | Port scanning for all ports, it takes too much time, you may need another switch, like -T5 ot -T4
-p	 | nmap 192.168.1.1 -p http,https	| Port scan from service name
-F  | nmap 192.168.1.1 -F	| Fast port scan (100 ports)
–top-ports  | nmap 192.168.1.1 –top-ports 2000	| Port scan the top X ports stated by the user
-p-65535  | nmap 192.168.1.1 -p-65535	| Leaving off initial port in range makes the scan start at port 1
-p0-	 | nmap 192.168.1.1 -p0-	| Leaving off end port in range makes the scan go through to port 65535



### Switches for the different techniques


Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-sS	| nmap 192.168.1.1 -sS	| TCP SYN port scan (Default)
-sT	| nmap 192.168.1.1 -sT	| TCP connect port scan (Default without root privilege)
-sU	| nmap 192.168.1.1 -sU	| UDP port scan
-sA	| nmap 192.168.1.1 -sA	| TCP ACK port scan
-sW	| nmap 192.168.1.1 -sW	| TCP Window port scan
-sM	| nmap 192.168.1.1 -sM	| TCP Maimon port scan


#### Switches for version and service detection


Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-sV	| nmap 192.168.1.1 -sV	| Attempts to determine the version of the service running on port
-sV –version-intensity	| nmap 192.168.1.1 -sV –version-intensity 8	| Intensity level 0 to 9. Higher number increases possibility of correctness
-sV –version-light	| nmap 192.168.1.1 -sV –version-light	| Enable light mode. Lower possibility of correctness. Faster
-sV –version-all	| nmap 192.168.1.1 -sV –version-all	| Enable intensity level 9. Higher possibility of correctness. Slower
-A	| nmap 192.168.1.1 -A	| Enables OS detection, version detection, script scanning, and traceroute




