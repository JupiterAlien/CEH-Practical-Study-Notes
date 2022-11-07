## Useful queries when analyzing packets in Wireshark


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
eq| == | Equal | ip.src == 10.10.10.100
