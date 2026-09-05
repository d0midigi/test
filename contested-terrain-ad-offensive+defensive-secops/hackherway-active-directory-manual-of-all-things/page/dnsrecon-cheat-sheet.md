# DNSRecon Cheat Sheet

COMMAND

DESCRIPTION

dnsrecon -d \<Target Domain> -j \<results json File>

Save results in a JSON file

dnscan.py -l $domains\_file -o outfile -w $wordlist

Subdomain brute-force of domains listed in a file (one by line)

dnscan.py -d target.com -o outfile -w $wordlist

Subdomain brute-force of a domain

dnssearch -domain \<Target Domain> -wordlist $wordlist

Dnssearch Subdomain brute-force

dnsrecon -d zonetransfer.me

Use Robin Wood’s zonetransfer.me site to enumerate and run a scan

dnsrecon -d zonetransfer.me -D \<namelist.txt> -t brt

Brute-force scan

dnsrecon -d zonetransfer.me -a

Zone Transfer

dnsrecon -d zonetransfer.me -a –db \~/Desktop/dnsrecon/dnsrecon-db

Look at SQLite database file

dnsrecon -d zonetransfer.me -a –xml \~/Desktop/dnsrecon/dnsrecon-xml

Save the results in XML format

dnsrecon -d TARGET -D /usr/share/wordlists/dnsmap.txt -t std –xml output.xml

DNS Zone Transfers

dnsrecon -d \<Target IP> -t std -D /usr/share/wordlists/dnsmap.txt

DNS (reverse) lookups / DNS Enumeration / Brute-force subdomains

$ python dnsrecon.py -n ns1.\<Target Domain> -d \<Target Domain> -D subdomains-top1mil-5000.txt -t brt

DNS enumeration tool

dnsrecon -w

DNS Reconnaissance

dnsrecon -r \<Target IP Range>

Reverse DNS Lookup on the target host

dnsrecon -t axfr -d \<Target Domain>

DNS Zone Transfer

dnsrecon -d \<Target Domain> -z

Zone enumeration against a target domain

dnsrecon -d \<Target Domain> -a ./dnsrecon.py -d \<Target Domain> -a

Or

dnsrecon -d \<Target Domain> -t axfr ./dnsrecon.py -d \<Target Domain> -t axfr

DNS Zone Transfer

dnsrecon -r \<Start Target IP>-\<End Target IP> ./dnsrecon.py -r \<Start Target IP>-\<End Target IP> ./dnsrecon.py -r \<Target IP Range>

Reverse Lookup against IP range

dnsrecon -d \<Target Domain> -s ./dnsrecon.py -d \<Target Domain> -s

Reverse lookup against all ranges in SPF records

dnsrecon -d \<Target Domain> -D \<namelist.txt> -t brt ./dnsrecon.py -d \<Target Domain> -D \<namelist> -t brt

Domain Brute-Force Enumeration

dnsrecon -d \<Target Domain> -D /usr/share/wordlists/dnsmap.txt -t std –xml output.xml

DNS Brute-Force

dnsrecon -t snoop -n \<Server IP> -D \<namelist.txt> ./dnsrecon.py -t snoop -n \<Server IP> -D \<dictionary file>

Cache Snooping against DNS NS (name servers)

dnsrecon -d \<Target Domain> ./dnsrecon.py -d \<Target Domain>

Standard Records Enumeration / Enumerate DNS records of targeted website

dnsrecon -d \<Target Domain> -t zonewalk

Zone Walking

dnsrecon -d \<Target Domain> -t rvl

Reverse Lookup of a given CIDR, network block, or IP range

dnsrecon -d \<Target Domain> -t brt -D \<Subdomains Dictionary>

Brute-force domains and hosts using a given dictionary

dnsrecon -d \<Target Domain> -t brt -D \<Subdomains Dictionary> --iw

Brute-force domains and hosts using a given dictionary. Continue brute-forcing a domain even if wildcard records are discovered

dnsrecon -d \<Target Domain> -t srv

SRV records

dnsrecon -d \<Target Domain> -t axfr

Test all NS servers for a zone transfer

dnsrecon -d \<Target Domain> -t goo

Google search for hidden subdomains and hosts of target domain

dnsrecon -d \<Target Domain> -t tld

Remove the TLD of a given domain and test against all TLDs registered in IANA

dnsrecon -d \<Target Domain> -t zonewalk

DNSSEC zone walk using NSEC records

dnsrecon -d \<Target Domain> --db \<results sqlite File>

Save results in a sqlite file

dnsrecon -d demo.com –xml \<results xml File>

Save results in an XML file

dnsrecon -d \<Target Domain> -c \<results csv file>

Save results in a CSV file

ARGUMENTS

-h, --help

Help message and exit

-d DOMAIN, --domain DOMAIN

Target domain parameters

-n NS\_SERVER, --name\_server NS\_SERVER

Domain server to use. If none are given, the SOA of the target will be used

-n nsserver.com

Use a custom NS (name server)

-r RANGE, --range RANGE

IP range for Reverse Lookup in brute-force formats (first-last) or in (range/bitmask)

-D DICTIONARY, --dictionary DICTIONARY

Dictionary file of subdomain and hostnames to use for brute-force. Filter out of brute-force domain lookup, records that resolve to the wildcard-defined IP address when saving records.

-f

Filter out of brute-force domain lookup, records that resolve to the wildcard-defined IP address when saving records

-t TYPE, --type TYPE

Type of enumeration to perform

-a

AXFR with standard enumeration

-r

Recursively scan subdomains

-s

Reverse lookup of IPv4 ranges in the SPF record with standard enumeration

-T

TLD expansion

-g

Google enumeration with standard enumeration

-b

Bing enumeration with standard enumeration

-k

Crt.sh enumeration with standard enumeration

-w

Deep WHOIS record analysis and reverse lookup of IP ranges found through WHOIS when doing a standard enumeration

-z

DNSSEC zone walk with standard enumeration

\--threads THREADS

Number of threads to use in reverse lookups, forward lookups, brute-force, and SRV record enumeration

\--lifetime LIFETIME

Time to wait for a server to respond to a query

\--tcp

Use TCP protocol to make queries

\--db DB

SQLite3 file to save found records/save results to SQLite database file

-x XML, --xml XML

XML file to save found records/save results to an XML file

-c CSV, --csv CSV

Comma-Separated Value file

-j JSON, --json JSON

JSON file

-i $file

Output discovered IP addresses to a text file

\--iw

Continue brute-forcing a domain even if wildcard records are discovered

-v

Enable verbose
