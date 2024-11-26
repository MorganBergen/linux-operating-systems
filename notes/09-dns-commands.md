#  linux dns commands

`resolvectl status` identifies the upstream dns server

`wget -qO- ifconfig.me/ip`  identifies your external ip address

`host`  dns lookup utility

`dig`  dns lookup utility

`whois`  conduct whois searches from the linux cli'


`apt update`  `apt install`  installs a command on your linux vm

##  a simplistic dns refresher

the domain name system (dns) is what resolves domain names to ip addresses for us.  in networking, servers are identified by ip addresses - not by their easy to remember domain names, so we need dns to make the internet more usable to us.  when you select a domain name in your search engine of choice (e.g. google, bing, etc), the browser asks the os to find the ip address of the domain.  after checking to make sure the resolution hasn't been cached at several different points, a dns query is sent (actually, several requests are sent from different servers) until an ip address is identified.  your computer then initiates a connection to the server at the identified ip address and you hopefully get the content you asked for.  this mostly happens behind the scenes.  

[bgp toolkit](https://bgp.he.net)

```
Welcome to the Hurricane Electric BGP Toolkit.

You are visiting from 2a09:bac2:628a:1250::1d3:5e United States

Announced as 2a09:bac2::/32 United States

Your ISP is AS13335 (Cloudflare, Inc.)
```

##  dns record types

`A`  address record ipv4 for domain name

`AAAA`  address record ipv6 address for domain name

`CNAME`  canonical name, basically an alias domain name

`PTR`  pointer record, domain name for an ip address

`MX`  mail exchanger, name of mail servers

`NS`  name servers, dns servers

`SOA`  start of authority, identifies primary name server

`TXT`  text notes, arbitrary notes, used `SPF`, `DKIM`, `DMARC`

##  email header analysis -  security

you will often find additional security information in email headers.  included among this information is 

**sender policy framework `SPF`**  

an anti-spoofing mechanism by which the sending organization can designate an authorized `MTA(s)` this is often reflected by a received-`SPF` line.  such lines will state whether the message passed or failed the `SPF` check.

**domain keys identified mail `DKIM`**

another mechanism to ensure the accuracy of an email by providing a digital signature of some or all of the email.

**domain-based message authentication, reporting, and conformance `DMARC`**

allows senders to suggest what should be done if `SPF` or `DKIM` check fail.

###  `cat /etc/resolv.conf`

view the default name servers in the `/etc/resolv.conf` file.

```bash
❯ cat /etc/resolv.conf
#
# macOS Notice
#
# This file is not consulted for DNS hostname resolution, address
# resolution, or the DNS query routing mechanism used by most
# processes on this system.
#
# To view the DNS configuration used by this system, use:
#   scutil --dns
#
# SEE ALSO
#   dns-sd(1), scutil(8)
#
# This file is automatically generated.
#
search hsd1.ca.comcast.net
nameserver 2001:558:feed::1
nameserver 2001:558:feed::2
nameserver 75.75.75.75
nameserver 75.75.76.76

~
```

###  `wget ipconfig.me`


##  `host` 

`host`  dns lookup utility

`$  host OPTION name/server`

host is a simple utility for performing dns lookups.  it is normally used to convert names to ip addresses and vice versa.  when no arguments or options are given, host prints a short summary of its command line argument and options.  

pertinent options 

`-t`  this option specifies the query type.  the type argument can be any recognized query type - `CNAME`, `NS`, `SOA`, `TXT`, `DNSKEY`, `AXFR`, etc.

```bash
❯ host google.com
google.com has address 172.217.164.110
google.com has IPv6 address 2607:f8b0:4005:80c::200e
google.com mail is handled by 10 smtp.google.com.
```

##  `nslookup`

`nslookup`  internet name servers interactively

`$ nslookup option [name] server`

`nslookup` is a program to query internet domain name servers.  `nslookup` has two modes - interactive and non-interactive.  interactive mode allows the user to query name servers for information about various hosts and domains ro to print a list of hosts in a domain.  non-interactive mode prints just the name and requested information for a host or domain.

pertinent options include

`-type=value`  this keyword changes the type of the information query to value.  the defaults are `A` and then `AAAA`, the abbreviations for these keywords are `q` and `ty`.

`nslookup`  starts the command in interactive mode.

```bash
❯ nslookup google.com
Server:		2001:558:feed::1
Address:	2001:558:feed::1#53

Non-authoritative answer:
Name:	google.com
Address: 142.250.189.174
```

##  `whois`

`whois`  client for the whois directory service

`$  whois OPTION OBJECT`  domain or ip address

`whois` searches for an object in an rfc 3912 database.  this version of the `whois` client tries to guess the right server to ask for the specified object.  if no guess can be made it will connect to `whois.networksoltions.com`, for `NIC` handles or `whois.arin.net` for ipv4 addresses and network names.

pertinent options include

`-H`  do not display the legal disclaimers that some registries like to show you.

`-I`  first query `whois.iana.org` and then follow its referral to the `whois` server authoritative for the request.

###  assessment

What is the IP Address of the upstream DNS server being used by your Cyber Range VM? Blank 1

`8.8.4.4`

What is the external IP address of your Cyber Range VM (HINT: as seen on the Internet)? Blank 1

`138.247.115.32`    

What are the kansas.gov name servers? (select all that apply)

`ks01.state.ks.us` && `ks11.state.ks.us`

Which one is designated as the Primary Name Server?

`ks01.state.ks.us`

What are the kansas.edu name servers? (select all that apply)

`ns-1068.awsdns-05.org` && `ns-621.awsdns-13.net` && `ns-51.awsdns-06.com`

What is the name of the Primary Name Server for kansas.edu?

`ns-1068.awsdns-05.org`

What is the name of the server at 205.251.192.51? Blank 1

`ns-51.awsdns-06.com`

What is the name of the mail server for emporia.edu? (either one) Blank 1

`cluster1.us.messagelabs.com` || `cluster1a.us.messagelabs.com`

Which of the following are IP addresses of the mail servers for emporia.edu? (choose all that apply)

`54.243.60.31` && `52.207.128.88` && `67.219.247.106`

Which IP addresses does emporia.edu designate as permitted senders under its SPF entry in DNS? (select the three that apply)

`23.21.109.212` && `198.248.132.13` && `12.228.6.215`