## DNS Types


#### A Record

The "A" stands for "address" and this is the most fundamental type of DNS record: it indicates the IP address of a given domain.
A records only hold IPv4 addresses. If a website has an IPv6 address, it will instead use an "AAAA" record.
For example, if you pull the DNS records of cloudflare.com, the A record currently returns an IP address of: 104.17.210.9.

#### AAAA Record

DNS AAAA records match a domain name to an IPv6 address. 
DNS AAAA records are exactly like DNS A records, except that they store a domain's IPv6 address instead of its IPv4 address.
As an example of the difference between IPv4 and IPv6 addresses, Cloudflare offers a public DNS resolver that anyone can use by setting their device's DNS to 1.1.1.1 and 1.0.0.1. 
These are the IPv4 addresses. The IPv6 addresses for this service are 2606:4700:4700::1111 and 2606:4700:4700::1001.

#### CNAME Record

The ‘canonical name’ (CNAME) record is used in lieu of an A record, when a domain or subdomain is an alias of another domain. 
All CNAME records must point to a domain, never to an IP address.

#### MX Record

These records resolve to the address of the servers that handle the email for the domain you are querying, for example an MX record response for facebook.com would look something like smtpin.vvv.facebook.com. 
These records also come with a priority flag. 
This tells the client in which order to try the servers, this is perfect for if the main server goes down and email needs to be sent to a backup server.

#### TXT Record

TXT records are free text fields where any text-based data can be stored. 
TXT records have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spam and spoofed email). 
They can also be used to verify ownership of the domain name when signing up for third party services.

