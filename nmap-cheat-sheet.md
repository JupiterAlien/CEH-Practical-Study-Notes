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
-Pn | nmap -Pn 192.168.1.1 | Doesn't bother pinging the host before scanning it. This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block
-f	| nmap 192.168.1.1 -f	| Requested scan (including ping scans) use tiny fragmented IP packets. Harder for packet filters
–-mtu	| nmap 192.168.1.1 –mtu 32	| Set your own offset size
-D	| nmap -D 192.168.1.101,192.168.1.102,192.168.1.103,192.168.1.23 192.168.1.1	| Send scans from spoofed IPs
-D	| nmap -D decoy-ip1,decoy-ip2,your-own-ip,decoy-ip3,decoy-ip4 remote-host-ip	| Above example explained
-S	| nmap -S www.microsoft.com www.facebook.com	| Scan Facebook from Microsoft (-e eth0 -Pn may be required)
-g	| nmap -g 53 192.168.1.1	| Use given source port number
–proxies	| nmap –proxies http://192.168.1.1:8080, http://192.168.1.2:8080 192.168.1.1	| Relay connections through HTTP/SOCKS4 proxies
–-data-length	| nmap –data-length 200 192.168.1.1	| Appends random data to sent packets
--scan-delay <time>ms | nmap --scan-delay <1000>ms | Used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
--badsum | nmap --badsum 192.168.1.1 | This one is used to generate an invalid checksum for packets

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


## Well-knwon ports list
There are 65535 ports, but only ports from 0 to 1023 are reserved for privileged services, and designated as well-known ports. 
Here's the list: 

Port # / Layer  |  Name                  |  Comment
--------------- | ---------------------- | ------------
1 |	tcpmux |	TCP port service multiplexer
5 |	rje |	Remote Job Entry
7 |	echo |	Echo service
9 |	discard |	Null service for connection testing
11 |	systat |	System Status service for listing connected ports
13 |	daytime |	Sends date and time to requesting host
17 |	qotd |	Sends quote of the day to connected host
18 |	msp |	Message Send Protocol
19 |	chargen |	Character Generation service; sends endless stream of characters
20 |	ftp-data |	FTP data port
21 |	ftp |	File Transfer Protocol (FTP) port; sometimes used by File Service Protocol (FSP)
22 |	ssh |	Secure Shell (SSH) service
23 |	telnet |	The Telnet service
25 |	smtp |	Simple Mail Transfer Protocol (SMTP)
37 |	time |	Time Protocol
39 |	rlp |	Resource Location Protocol
42 |	nameserver |	Internet Name Service
43 |	nicname |	WHOIS directory service
49 |	tacacs |	Terminal Access Controller Access Control System for TCP/IP based authentication and access
50 |	re-mail-ck |	Remote Mail Checking Protocol
53 |	domain |	domain name services (such as BIND)
63 |	whois++ |	WHOIS++, extended WHOIS services
67 |	bootps |	Bootstrap Protocol (BOOTP) services; also used by Dynamic Host Configuration Protocol (DHCP) services
68 |	bootpc |	Bootstrap (BOOTP) client; also used by Dynamic Host Control Protocol (DHCP) clients
69 |	tftp |	Trivial File Transfer Protocol (TFTP)
70 |	gopher |	Gopher Internet document search and retrieval
71 |	netrjs-1 |	Remote Job Service
72 |	netrjs-2 |	Remote Job Service
73 |	netrjs-3 |	Remote Job Service
73 |	netrjs-4 |	Remote Job Service
79 |	finger |	Finger service for user contact information
80 |	http |	HyperText Transfer Protocol (HTTP) for World Wide Web (WWW) services
88 |	kerberos |	Kerberos network authentication system
95 |	supdup |	Telnet protocol extension
101 |	hostname |	Hostname services on SRI-NIC machines
102/tcp |	iso-tsap |	ISO Development Environment (ISODE) network applications
105 |	csnet-ns |	Mailbox nameserver; also used by CSO nameserver
107 |	rtelnet |	Remote Telnet
109 |	pop2 |	Post Office Protocol version 2
110 |	pop3 |	Post Office Protocol version 3
111 |	sunrpc |	Remote Procedure Call (RPC) Protocol for remote command execution, used by Network Filesystem (NFS)
113 |	auth |	Authentication and Ident protocols
115 |	sftp |	Secure File Transfer Protocol (SFTP) services
117 |	uucp-path |	Unix-to-Unix Copy Protocol (UUCP) Path services
119 |	nntp |	Network News Transfer Protocol (NNTP) for the USENET discussion system
123 |	ntp |	Network Time Protocol (NTP)
137 |	netbios-ns |	NETBIOS Name Service used in Red Hat Enterprise Linux by Samba
138 |	netbios-dgm |	NETBIOS Datagram Service used in Red Hat Enterprise Linux by Samba
139 |	netbios-ssn |	NETBIOS Session Service used in Red Hat Enterprise Linux by Samba
143 |	imap |	Internet Message Access Protocol (IMAP)
161 |	snmp |	Simple Network Management Protocol (SNMP)
162 |	snmptrap |	Traps for SNMP
163 |	cmip-man |	Common Management Information Protocol (CMIP)
164 |	cmip-agent |	Common Management Information Protocol (CMIP)
174 |	mailq |	MAILQ email transport queue
177 |	xdmcp |	X Display Manager Control Protocol (XDMCP)
178 |	nextstep |	NeXTStep window server
179 |	bgp |	Border Gateway Protocol
191 |	prospero |	Prospero distributed filesystem services
194 |	irc |	Internet Relay Chat (IRC)
199 |	smux |	SNMP UNIX Multiplexer
201 |	at-rtmp |	AppleTalk routing
202 |	at-nbp |	AppleTalk name binding
204 |	at-echo |	AppleTalk echo
206 |	at-zis |	AppleTalk zone information
209 |	qmtp |	Quick Mail Transfer Protocol (QMTP)
210 |	z39.50 |	NISO Z39.50 database
213 |	ipx |	Internetwork Packet Exchange (IPX), a datagram protocol commonly used in Novell Netware environments
220 |	imap3 |	Internet Message Access Protocol version 3
245 |	link |	LINK / 3-DNS iQuery service
347 |	fatserv |	FATMEN file and tape management server
363 |	rsvp_tunnel |	RSVP Tunnel
369 |	rpc2portmap |	Coda file system portmapper
370 |	codaauth2 |	Coda file system authentication services
372 |	ulistproc |	UNIX LISTSERV
389 |	ldap |	Lightweight Directory Access Protocol (LDAP)
427 |	svrloc |	Service Location Protocol (SLP)
434 |	mobileip-agent |	Mobile Internet Protocol (IP) agent
435 |	mobilip-mn |	Mobile Internet Protocol (IP) manager
443 |	https |	Secure Hypertext Transfer Protocol (HTTP)
444 |	snpp |	Simple Network Paging Protocol
445 |	microsoft-ds |	Server Message Block (SMB) over TCP/IP
464 |	kpasswd |	Kerberos password and key changing services
468 |	photuris |	Photuris session key management protocol
487 |	saft |	Simple Asynchronous File Transfer (SAFT) protocol
488 |	gss-http |	Generic Security Services (GSS) for HTTP
496 |	pim-rp-disc |	Rendezvous Point Discovery (RP-DISC) for Protocol Independent Multicast (PIM) services
500 |	isakmp |	Internet Security Association and Key Management Protocol (ISAKMP)
535 |	iiop |	Internet Inter-Orb Protocol (IIOP)
538 |	gdomap |	GNUstep Distributed Objects Mapper (GDOMAP)
546 |	dhcpv6-client |	Dynamic Host Configuration Protocol (DHCP) version 6 client
547 |	dhcpv6-server |	Dynamic Host Configuration Protocol (DHCP) version 6 Service
554 |	rtsp |	Real Time Stream Control Protocol (RTSP)
563 |	nntps |	Network News Transport Protocol over Secure Sockets Layer (NNTPS)
565 |	whoami |	whoami user ID listing
587 |	submission |	Mail Message Submission Agent (MSA)
610 |	npmp-local |	Network Peripheral Management Protocol (NPMP) local / Distributed Queueing System (DQS)
611 |	npmp-gui |	Network Peripheral Management Protocol (NPMP) GUI / Distributed Queueing System (DQS)
612 |	hmmp-ind |	HyperMedia Management Protocol (HMMP) Indication / DQS
631 |	ipp |	Internet Printing Protocol (IPP)
636 |	ldaps |	Lightweight Directory Access Protocol over Secure Sockets Layer (LDAPS)
674 |	acap |	Application Configuration Access Protocol (ACAP)
694 |	ha-cluster |	Heartbeat services for High-Availability Clusters
749 |	kerberos-adm |	Kerberos version 5 (v5) ‘kadmin’ database administration
750 |	kerberos-iv |	Kerberos version 4 (v4) services
765 |	webster |	Network Dictionary
767 |	phonebook |	Network Phonebook
873 |	rsync |	rsync file transfer services
992 |	telnets |	Telnet over Secure Sockets Layer (TelnetS)
993 |	imaps |	Internet Message Access Protocol over Secure Sockets Layer (IMAPS)
994 |	ircs |	Internet Relay Chat over Secure Sockets Layer (IRCS)
995 |	pop3s |	Post Office Protocol version 3 over Secure Sockets Layer (POP3S)



