## Useful dig switches

Dig – Domain Information Groper is a light weight Linux utility for querying DNS records. 
It is widely used to diagnose DNS servers, troubleshoot DNS servers, purge DNS Cache using external DNS server and dozen of great features it provides.

Dig Commands List

Switch          | Example                | Description
--------------- | ---------------------- | ------------
dig -x <TargetDomain> | dig google.com | Lookups – mapping names to addresses
dig -x <Target IP> | dig -x 192.168.0.10 | Reverse lookups – mapping addresses to names
dig @<Target server host> | dig @8.8.8.8 google.com | Lookups at DNS Server
dig @<Target server host> -x IP | dig @8.8.8.8 -x 74.72.72.71 | Lookups at DNS Server
dig <TargetDomain> any | dig google.com any | Lookup for an any record (TXT, MX, SOA, A, NS)
dig HOST soa | dig google.com soa | Lookup for an soa record
dig HOST ns | dig google.com ns | Lookup for an ns record
dig HOST a | dig google.com a | Lookup for an a record
dig HOST mx | dig google.com mx | Lookup for an mx record
dig HOST txt | dig google.com txt | Lookup for an txt record
dig +trace <TargetDomain> | dig +trace google.com OR dig +trace -x 173.252.120.6 | Lookup with trace
  
  
 
