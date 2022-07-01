# NMAP Cheat Sheet

## Useful switches for nmap during reconnaissance. 

This one here is quite effective, it scans all the open ports (-p- --open) using a SYN scan, and its just sends 5000 packets per second, it leverages the triple verbose switch to display the ports found in the console during the scan, and it doesn't wait for the DNS resolution. And the output comes in a grepable format.
Please keep in mind that due to switches, this command needs to be ran as sudo.

    nmap -p- --open -sS --min-rate 5000 -vvv -Pn <TARGET-IP> -oG <OUTPUT-FILE-NAME>


### Port Specification Switches


Switch          | Example                | Description
--------------- | ---------------------- | ------------
-P  | nmap -p 23 192.168.1.1 | Port scanning for an specific port
-P  | nmap -p 23-100 192.168.1.1 | Port scanning for an specific range of ports 
-p  | nmap -U:110,T:443 192.168.1.1 | Scanning different port types by UDP (U) or TCP (T)
-p-  | nmap -p- 192.168.1.1 | Port scanning for all ports, it takes too much time, you may need another switch, like -T5 ot -T4
-p	 | nmap 192.168.1.1 -p http,https	| Port scan from service name
-F  | nmap 192.168.1.1 -F	| Fast port scan (100 ports)
–top-ports  | nmap 192.168.1.1 –top-ports 2000	| Port scan the top X ports stated by the user
-p-65535  | nmap 192.168.1.1 -p-65535	| Leaving off initial port in range makes the scan start at port 1
-p0-	 | nmap 192.168.1.1 -p0-	| Leaving off end port in range makes the scan go through to port 65535




### Switches for timing and performance

Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-T0 | nmap 192.168.1.1 -T0	| Paranoid (0) Intrusion Detection System evasion
-T1	| nmap 192.168.1.1 -T1	| Sneaky (1) Intrusion Detection System evasion
-T2	| nmap 192.168.1.1 -T2	| Polite (2) slows down the scan to use less bandwidth and use less target machine resources
-T3	| nmap 192.168.1.1 -T3	| Normal (3) which is default speed
-T4	| nmap 192.168.1.1 -T4	| Aggressive (4) speeds scans; assumes you are on a reasonably fast and reliable network
-T5	| nmap 192.168.1.1 -T5	| Insane (5) speeds scan; assumes you are on an extraordinarily fast network




### Switches for the different techniques/types


Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-sS	| nmap 192.168.1.1 -sS	| TCP SYN port scan (Default)
-sT	| nmap 192.168.1.1 -sT	| TCP connect port scan (Default without root privilege)
-sU	| nmap 192.168.1.1 -sU	| UDP port scan
-sA	| nmap 192.168.1.1 -sA	| TCP ACK port scan
-sW	| nmap 192.168.1.1 -sW	| TCP Window port scan
-sM	| nmap 192.168.1.1 -sM	| TCP Maimon port scan
-Sf | nmap -Sf 192.168.1.1  | TCP FIN scan, sets just the TCP FIN bit.
-sX | nmap -sX 192.168.1.1  | XMAS scan, sets the FIN, PSH, and URG flags, lighting the packet up like a Christmas tree.
-sN | nmap -sN 192.168.1.1  | TCP null scan, does not send any bits (TCP flag header is 0)
-sP | nmap -sP 192.168.1.1. | Ping scans the network, listing machines that respond to ping. You can use /mask
-sL | nmap -sL 192.168.1.1  | Simply list targets to scan




### Switches for version and service detection


Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-sV	| nmap 192.168.1.1 -sV	| Attempts to determine the version of the service running on port
-sV –version-intensity	| nmap 192.168.1.1 -sV –version-intensity 8	| Intensity level 0 to 9. Higher number increases possibility of correctness
-sV –version-light	| nmap 192.168.1.1 -sV –version-light	| Enable light mode. Lower possibility of correctness. Faster
-sV –version-all	| nmap 192.168.1.1 -sV –version-all	| Enable intensity level 9. Higher possibility of correctness. Slower
-A	| nmap 192.168.1.1 -A	| Enables OS detection, version detection, script scanning, and traceroute




### Switches for Operating System detection

Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-O	| nmap 192.168.1.1 -O	| Remote OS detection using TCP/IP stack fingerprinting
-O –osscan-limit	| nmap 192.168.1.1 -O –osscan-limit	| If at least one open and one closed TCP port are not found it will not try OS detection against host
-O –osscan-guess	| nmap 192.168.1.1 -O –osscan-guess	| Makes Nmap guess more aggressively
-O –max-os-tries	| nmap 192.168.1.1 -O –max-os-tries 1	| Set the maximum number x of OS detection tries against a target
-A	| nmap 192.168.1.1 -A	| Enables OS detection, version detection, script scanning, and traceroute



### Switches for Firewall/IDS Evasion and Spoofing

Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-f	| nmap 192.168.1.1 -f	| Requested scan (including ping scans) use tiny fragmented IP packets. Harder for packet filters
–mtu	| nmap 192.168.1.1 –mtu 32	| Set your own offset size
-D	| nmap -D 192.168.1.101,192.168.1.102,192.168.1.103,192.168.1.23 192.168.1.1	| Send scans from spoofed IPs
-D	| nmap -D decoy-ip1,decoy-ip2,your-own-ip,decoy-ip3,decoy-ip4 remote-host-ip	| Above example explained
-S	| nmap -S www.microsoft.com www.facebook.com	| Scan Facebook from Microsoft (-e eth0 -Pn may be required)
-g	| nmap -g 53 192.168.1.1	| Use given source port number
–proxies	| nmap –proxies http://192.168.1.1:8080, http://192.168.1.2:8080 192.168.1.1	| Relay connections through HTTP/SOCKS4 proxies
–data-length	| nmap –data-length 200 192.168.1.1	| Appends random data to sent packets


### Switches for outputs

Switch          | Example	               | Description
--------------- | ---------------------- | ------------
-oN	| nmap 192.168.1.1 -oN normal.file	| Normal output to the file normal.file
-oX	| nmap 192.168.1.1 -oX xml.file	| XML output to the file xml.file
-oG	| nmap 192.168.1.1 -oG grep.file	| Grepable output to the file grep.file
-oA	| nmap 192.168.1.1 -oA results	| Output in the three major formats at once
-oG –	| nmap 192.168.1.1 -oG –	| Grepable output to screen. -oN -, -oX – also usable
–append-output	| nmap 192.168.1.1 -oN file.file –append-output	| Append a scan to a previous scan file
-v	| nmap 192.168.1.1 -v	| Increase the verbosity level (use -vv or more for greater effect)
-d	| nmap 192.168.1.1 -d	| Increase debugging level (use -dd or more for greater effect)
–reason	| nmap 192.168.1.1 –reason	| Display the reason a port is in a particular state, same output as -vv
–open	| nmap 192.168.1.1 –open	| Only show open (or possibly open) ports
–packet-trace	| nmap 192.168.1.1 -T4 –packet-trace	| Show all packets sent and received
–iflist	| nmap –iflist	| Shows the host interfaces and routes
–resume	| nmap –resume results.file	| Resume a scan


