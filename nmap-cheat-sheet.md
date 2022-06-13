# NMAP Cheat Sheet

## Useful switches for nmap during reconnaissance. 

#### Port Specification Switches

Syntax          | Example                | Description
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
