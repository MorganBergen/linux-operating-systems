#  network commands

`ip`  show and manage ip addresses, network interfaces, and routes

`ping`  check network connections via `IMAP` protocol

`ss` investigate network sockets

##  `ip`

`ip`  show / manipulate routing, network devices, interfaces, and tunnels

`$ ip [OPTIONS] OBJECT COMMAND`

this is an extensive linux command that replaced many deprecated commands, some of which were commonly used. 

pertinent options include

`-h`  output statistics with human readable values followed by suffix

`-s`  output more information.  if the option appears twice or more, the amount of information increases.  as a rule, the information statistics or some time values.

`-d`  output more detailed information

`-r`  use the systems name resolver to print dns names instead of host addresses

`-j`  output results in javascript object notation `JSON` can use `-p` with it

`-6`  shortcut for `-family inet6`

pertinent `OBJECT` and the command they replaced

`a/addr/address`  protocol `IP` or `IPv6` address on a device `ifconfig`

`l/link`  manage network interfaces `ifconfig`

`n/neigh/neighbor`  manage ARP cache entries `arp`

##  `ping`

`ping`  send `ICMP ECHO_REQUEST` to network hosts

`$ ping [option] <destination>`

`ping` uses the `ICMP` protocol's mandatory `ECHO_REQUEST` datagrams to elicit an `ICMP ECHO_RESPONSE` from a host or gateway.  `ECHO_REQUEST` datagrams `ping` have an `IP` and `ICMP` header, followed by a struct timeval and then an arbitrary number of `pad` bytes used to fill out the packet

pertinent options include

`-c`  stop after sending count `ECHO_REQUEST` packets

`-w`  specify a timeout, in seconds, before ping exists regardless of how many packets have been sent or received

`-6`  use `IPv6` only

##  `ss`

`ss`  another utility to investigate sockets  `netstat`

`$ ss [OPTIONS] [ FILTER ]`

`ss` is used to dump socket statistics.  it allows showing information similar to `netstat`.  it can display more `TPC` and state information than other tools

pertinent options include

`-n`  don't resolve service names

`-a`  display all sockets

`-I`  display listening sockets

`-e`  show detailed socket information

`-s`  show socket usage summary

`-4`  display only ip version 4 sockets

`-6`  display only ip version 6 sockets

`-t`  display only tcp sockets

`-u`  display only udp sockets

you can append state filters to the end of the command with `state [FILTER]`.  filters include all, connected, synchronized, but also include tcp states such as `established`, `syn-sent`, `syn-recv`, `fin-wait-{1,2}`, `time-wait`, `closed`, `close-wait`, `last-ack`, `listening`, `closing`

##  assessment

What is the name of the Ethernet interface on your Cyber Range VM?

`ens160`

What IPv4 IP address is assigned to the Ethernet interface on your Cyber Range VM? Blank 1

`172.20.12.150`

What is the Broadcast IPv4 Address assigned to your Ethernet interface? Blank 1

`172.20.12.255`

What is the IPv4 DNS name of the Ethernet interface on your Cyber Range VM?

`student-virtual-machine`

What is the MAC address of the device to which 172.20.12.1 is assigned? Blank 1

`00:1B:17:00:01:01`

What is the IPv4 IP address of the loopback/localhost interface on your Cyber Range VM?

`127.0.0.1`

by default, how many pings will the Linux ping command send?

`Unlimited, until you stop it with SIGNINT`

how many IPv4 TCP ports are listening on your Cyber Range VM?

`two`

what are the listening IPv4 TCP ports on your Cyber Range VM? (select all that apply)

`631`, `53`

which IPv4 UDP port on your Cyber Range VM has an established connection with (to) 172.20.12.1?

`68`
