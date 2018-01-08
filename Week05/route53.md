# ROUTE 53
## BASICS
- Name origin in the default udp port for dns 53
- SLA uptime of 100% https://en.wikipedia.org/wiki/Service-level_agreement.
- DNS => Mapping of human friendly domain names to internet protocols (IP)
- IPv4 (old school: 32bit field) 4 billions of addresses IPv6 (128bits field) 340 undecillion
- domain names => .com .gov second level domain names => .co.cr
- top level domain names are controlled by iana https://www.iana.org/domains/root/db
- A Register that can assing domains for a top level domain names (ex godaddy) that register with InterNIC, a service of ICANN in a central database known as WhoIs.
- There is no relationship between IP Subnets and subdomains.
- A zone comprises all the data for a given domain except those parts of the domain that are delegated to other name servers.
- A name server can be authoritative for a zone. This means the server has full information about the zone.  A single name server can manage many different zones.
- Zones also fall into two categories: primary master or secondary master. A primary master maintains (create and modify records) the original records for the zone. Secondary master is a backup copy updaten periodically.


## DOMAINS
- Record domains.
- Transfer domains.
- Hosted zone is automatically created tho you may route your DNS queries to another DNS provider.
- A hosted zone contains information about how you want to route your traffic both for your domain and for any subdomains that you may have
- If you are not using Amazon Route 53 as the domain registrar, then you will need to create a hosted zone

## RECORDS
### SOA (Start of authority)
- Name of the server that supplied data (authorative) for the zone.
- The administrator of the zone.
- Current version of data file
- The number of seconds a secondary name server should wait before checking for updates
- The number of seconds a secondary name server should wait before retrying a failed zone
- The maximum number of seconds that a secondary name server can use data before it must either be refreshed or expired.
- The default number for seconds for the time-to-live (ttl) file on resource records.
- TTL: The length in seconds the dns record is cached on either the resolving servers or the users own local pc.
- Most TTL are set for 2 days

### NS (Name server)
- Used by top level domain servers to direct trafic to the Content DNS server which contains the authorative DNS records
- These are the records that has to be registered with your register ex. godaddy

### A
- Is the fundamental type of dns record that maps a domain to a IP Address.

### CName (Canonical Name)
- Resolve one domain name to another

### Pointer (PTR)
- A reverse of an A Record
- Maps IP Address to DNS

### MX
- To route email.
- An MX record includes the Fully Qualified Domain Name(FQDN) of the mail server for the zone.
- The preference number(0-65535) establishes priority for mail.  Multiple MX records with different preference numbers, the one with the lowest number is attempted first.

### Sender Policy Framework SPF
- To prevent spam
- Tells the mail server which ip can send mails from your domain.

### Service (SRV)
- It is a specification of data in the DNS defining the location (host name and port number) of servers for specified services.
- Example for a domain name example.com and service name web[HTTP] running on a TCP protocol. A DNS query can be issued to find the host name that provides that service.

### Alias Record
- Created by AWS.
- Use to map resource record sets to ELB, Cloud Front distributions or S3 buckets.
- Similar to CName, but it can be used for naked domains.
- Amazon Route 53 automatically recognizes changes in the record sets that the aliases resource record set refers to.

## ROUTING POLICIES

### SIMPLE
- Round Robin assignment

### WEIGHTED ROUTING
- proportional: weight / Sum of weights
- use case: AB Testing
- calculated during the lenght of the day.

### LATENCY BASED 
- For applications hosted in multiple Amazon EC2 regions.
- Aws keeps records of latency and send to the lowest.
- The region is selected manually.
- Latency-based routing is based on latency measurements performed over a period of time, 

### GEOLOCATION
- Routes the traffic depending on the geographic location of the user.
- If no default and the zone is not register, traffic is not routed.
- use case: personalization.

### FAILOVER
- Pasive/Active set up.
- First, need to create a healthcheck to the resource.
- Select the primary with a healthcheck.
- Select the secondary as failover (no healthcheck).

### MULTIVALUE ANSWER ROUTING
- Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.
- Only healthy ips are returned.

## EXAM TIPS
- ELB does not have a IPv4, only DNS
- You are charged for the request to CName but not for the Alias.

## MISC
- When creating a route, name input can be empty => nacked domain.

## RESOURCES
- https://www.techrepublic.com/article/understanding-how-dns-works-part-1/
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html
- https://aws.amazon.com/route53/pricing/
