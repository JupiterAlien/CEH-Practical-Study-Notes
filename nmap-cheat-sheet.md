# NMAP Cheat Sheet

## Useful switches for nmap during reconnaissance. 

#### Port Specification Switches

Syntax          | Example       | Description
--------------- | ------------- | ------------
-P | nmap -p 23 192.168.1.10 | Port scanning for an specific port
-P | nmap -p 23-100 192.168.1.10 | Port scanning for an specific range of ports 
-p | nmap -U:110,T:443 192.168.1.10 | Scanning different port types by UDP (U) or TCP (T)
-p- | nmap -p- 192.168.1.10 | Port scanning for all ports, it takes too much time, you may need another switch, like -T5 ot -T4
