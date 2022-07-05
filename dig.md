## Useful dig switches

Dig – Domain Information Groper is a light weight Linux utility for querying DNS records. 
It is widely used to diagnose DNS servers, troubleshoot DNS servers, purge DNS Cache using external DNS server and dozen of great features it provides.

Dig Commands List

Switch          | Example                | Description
--------------- | ---------------------- | ------------
dig -x TARGET | dig google.com | Lookups – mapping names to addresses
dig -x TARGET | dig -x 192.168.0.10 | Reverse lookups – mapping addresses to names
dig @TARGET | dig @8.8.8.8 google.com | Lookups at DNS Server
dig @TARGET -x IP | dig @8.8.8.8 -x 74.72.72.71 | Lookups at DNS Server
dig TARGET any | dig google.com any | Lookup for an any record (TXT, MX, SOA, A, NS)
dig TARGET soa | dig google.com soa | Lookup for an soa record
dig TARGET ns | dig google.com ns | Lookup for an ns record
dig TARGETa | dig google.com a | Lookup for an a record
dig TARGET mx | dig google.com mx | Lookup for an mx record
dig TARGET txt | dig google.com txt | Lookup for an txt record
dig +trace TARGET | dig +trace google.com  OR dig +trace -x 173.252.120.6 | Lookup with trace


  
 
