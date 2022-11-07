## Useful queries when analyzing packets in Wireshark


Wireshark documentation: https://www.wireshark.org/docs/dfref/d/dns.html


**Capture Filters**: This type of filter is used to save only a specific part of the traffic. It is set before capturing traffic and not changeable during the capture. 


**Display Filters**: This type of filter is used to investigate packets by reducing the number of visible packets, and it is changeable during the capture. 


#### Capture Filter Syntax

These filters use byte offsets hex values and masks with boolean operators, and it is not easy to understand/predict the filter's purpose at first glance. The base syntax is explained below:

    Scope: host, net, port and portrange.
    Direction: src, dst, src or dst, src and dst,
    Protocol: ether, wlan, ip, ip6, arp, rarp, tcp and udp.
    Sample filter to capture port 80 traffic: tcp port 80

#### Comparison Operators


Name | Syntax | Description | Example
-----|--------|-------------|--------
eq| == | Equal | ip.src == 192.169.10.100
ne | != | Not equal | ip.src != 10.10.10.100
gt | > | Greater than | ip.ttl > 250
lt | < | Less than | ip.ttl < 10
ge | >= | Greater or equal than | ip.ttl >= 0xFA
le | <= | Less or equal than | ip.ttl <= 0xA


#### Logical Operators

Name | Syntax | Description | Example
-----|--------|-------------|--------
and | && | Logical AND | (ip.src == 10.10.10.100) AND (ip.src == 10.10.10.111)
or | Double pipe | Logical OR | (ip.src == 10.10.10.100) OR (ip.src == 10.10.10.111)
not | ! | Logical NOT | !(ip.src == 10.10.10.222)


### Exclude IP address: remove traffic from and to IP address
!ip.addr ==192.168.0.1

### Display traffic between two specific subnet
ip.addr == 192.168.0.1/24 and ip.addr == 192.168.1.1/24

### Display traffic between two specific workstations
ip.addr == 192.168.0.1 and ip.addr == 192.168.0.2

### Filter by MAC
eth.addr = 00:90:7f:c5:b6:67

### Filter TCP port
tcp.port == 80

### Filter TCP port source
tcp.srcport == 80

### Filter TCP port destination
tcp.dstport == 80

### Find user agents
http.user_agent contains Firefox
!http.user_agent contains || !http.user_agent contains Chrome

### Filter broadcast traffic
!(arp or icmp or dns)

### Filter IP address and port
tcp.port == 80 && ip.addr == 192.168.0.1

### Filter all http get requests
http.request

### Filter all http get requests and responses
http.request or http.response

### Filter three way handshake
tcp.flags.syn==1 or (tcp.seq==1 and tcp.ack==1 and tcp.len==0 and tcp.analysis.initial_rtt)

### Find files by type
frame contains “(attachment|tar|exe|zip|pdf)”

### Find traffic based on keyword
tcp contains google
frame contains twitter

### Detecting SYN Floods
tcp.flags.syn == 1 and tcp.flags.ack == 0

