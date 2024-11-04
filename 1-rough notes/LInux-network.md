# Linux-network
---
Date: 07,Oct,2024
subject:  networking related commands on linux
field: [[linux]] [[networking]]
tags: #ping #wget #curl #dig #traceroute #whois #hostname

---
---

# PING
- the most common command which even a kid knows
- it determines the reachability  of a server.
- it measures the time it takes for packet to travel from host to destination to back to host, giving info about network's latency and any packet loss
-  **ping [option] hostname/ipaddr**
- ping sends a series of ICMP packets.

```bash
ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=58 time=7.87 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=58 time=7.37 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=58 time=7.98 ms

--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 7.239/9.805/14.366/2.833 ms


ping -c 4 1.1.1.1 = specify number of requests


```
In this output:

- `64 bytes from 1.1.1.1`: Indicates that a packet of 64 bytes was received from that IP address.
- `icmp_seq`: Sequence number of the echo request.
- `ttl`: Time to live, showing how many hops the packet can make before being discarded.
- `time`: The round-trip time for the packet in milliseconds.

#  TraceRoute

- a tool that track the path of a packet from source to destinatin
- packets are sent out with progressively increasing  TTL.


fields:  Hop numer   :    hostname/ip    :  round trip time RTT

TTL = **Time To Live**  is a method of limiting the lifespan of data. for ip packets, the TTL is a counter that decreases for every hop that the data passes on its way to the destination.

RTT = **Round Trip Time** is the time taken by a packet from the source to destination then back to the source



now trace route is a cleaver piece of shit, what it does is it progressively increase the ttl value of packet
	1. it will first send the first packet with ttl 1
	2. now when this packet reaches to the router, ttl value becomes 1 to 0, so router respond with ttl exceeded.
	3. now traceroute take note of that ip and now again send a packet but with ttl value of 2, so when it reaches 1st router, ttl become 1, and so it will forward the packet to next router , and then ttl will again be 0 and traceroute will recieve another ttl exceeded and again takes note of its ip and keep repeating this process
	4. traceroute will keep doing this untill it reaches the destination or traceroute reaches max hop which is usually 30

- traceroute by default sends 3 packets to each hop to maintain get a very consistant and reliable data or detect any packet loss, all 3 packets would have similar RTT but if there is a big gap, it would show either theres some congestion in the network or queueing delay.


 -   * * * shows there was no response from that hop so no RTT also

```bash
traceroute to google.com (142.250.194.174), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.529 ms  0.710 ms  0.889 ms
 2  10.72.95.1 (10.72.95.1)  3.642 ms  3.919 ms  4.123 ms
 3  * * *
 4  103.240.232.1 (103.240.232.1)  8.560 ms  8.376 ms  8.082 ms
 5  74.125.118.188 (74.125.118.188)  8.786 ms  9.105 ms  9.747 ms
 6  * * *
 7  142.251.54.82 (142.251.54.82)  6.791 ms 142.251.54.100 (142.251.54.100)  7.177 ms 142.251.52.216 (142.251.52.216)  8.181 ms
 8  192.178.83.206 (192.178.83.206)  7.872 ms 192.178.82.232 (192.178.82.232)  8.001 ms 142.251.52.219 (142.251.52.219)  7.697 ms
 9  del12s06-in-f14.1e100.net (142.250.194.174)  8.396 ms 216.239.62.181 (216.239.62.181)  9.160 ms del12s06-in-f14.1e100.net (142.250.194.174)  8.210 m
```


```bash

traceroute 1.1.1.1 = default

traceroute -n 1.1.1.1 = without hostname mapping

traceroute -q 5 1.1.1.1 = define the packet number (default 3, max 10)

```


# HOSTNAME
- Hostname command is used to display or set the hostname of a device
- hostname is name given to a system to identify it on a network

```bash
hostname = display the current hostname

hostname newhostname = will channge hostname temporarily, only last until next reboot

hostname -f = display FQDN of system
```


- to permanently change the hostname
- edit `/etc/hostname`
- edit `/etc/hosts` to  resolve the new hostname to 127.0.0.1 
- restart system or `1. sudo systemctl restart systemd-hostnamed`

### /etc/hosts

/etc/hosts is a text file in unix like OS which maps the hostname to ip adderss locally. it acts as a local dns system allowing our OS to resolve a hostname to an IP address.

in linux when  a program tries to resolve the hostname, system will first check the /etc/hosts to check for any entry. if the hostname is found, corresponding IP will be returned

if not then system will proceed to query the DNS server specified in `/etc/resolve.conf

```bash
an example of /etc/hosts, if we curl these hostnames, it will go to these ip

127.0.0.1   localhost
127.0.1.1   mymachine
192.168.1.10   webserver1.local  webserver1
10.0.0.5   dbserver.local  dbserver

```

- we can use it as a simple blocklist of domains by routing them to loopback address.
- we can rename our localhost to anything 
- now curl and browser will have different behaviour cause of SSL/TLS so mostly only useful in testing purpose but its cool

### /etc/resolve.conf
the `/etc/resolve.conf` is an important file which tells the system about which server to use to resolve  hostname into IP. whenever we try to connect to a domain, our system uses this file to get IP of server that will resolve the hostname into ip

```bash 
nameserver 1.1.1.1
nameserver 8.8.8.8
```

by default it will use `1.1.1.1` to resolve the hostnames but if this will fail
it will use `8.8.8.8` as a fallback to resolve hostname


# WHOIS

**WHOIS** is a utility used to get detailed info about owner and registration of a domain or ip address.  its commonly used for domain research, domain registration details.

- it query a remote whois database to get information
- **Domain Ownership Verification**: Check who owns a domain name and whether it’s available for purchase or registration.
- **Domain Expiration**: Determine when a domain is set to expire, which can be useful for domain monitoring.
- **IP Address Research**: Find out more about the organization responsible for a particular IP address.
- **Security Investigations**: In cybersecurity, the `whois` command is used to track down information about domain names and IPs involved in suspicious activity.
#### Privacy Considerations

Due to privacy regulations like **GDPR** (General Data Protection Regulation), many `whois` records, particularly for personal or non-corporate domains, may have obfuscated or hidden personal information. You'll often see entries like "REDACTED FOR PRIVACY" or "Data Protected" instead of specific contact details.

```bash
whois google.com
whois 1.1.1.1
```


# DIG
Domain Information Groper is a network tool used for qureying DNS server to get info about dns record, domain name, ip.

```bash
dig google.com

; <<>> DiG 9.16.1-Ubuntu <<>> example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1234
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 0

;; QUESTION SECTION:
;example.com.                   IN      A

;; ANSWER SECTION:
example.com.            86400   IN      A       93.184.216.34

;; Query time: 23 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
;; WHEN: Wed Oct 11 12:34:56 2023
;; MSG SIZE  rcvd: 65

in this output, we have our ansewer section where we can see the resolved ip and in bottom SERVER shows the resolver ip which sent this request to actual server

```

```bash
dig ns google.com = specify DNS record type

dig google.com +short = only get the ip

dig google.com +noall +answer = only shows the anser section

dig -x 1.1.1.1 = reverse lookup

```


# CURL
Client URL (curl) is a tool used for transferring data to and from a server using protocols like HTTP, HTTPS, FTP, etc.

```bash

curl OPTIONS URL

curl http://example.com

curl -o http://example.com/file.zip = save output

curl -L http://example.com = follow redirects

curl -I http://example.com = show only headers
```


*i dont even use it much except curling localhost*


# WGET
- `wget` is a command-line utility used to download files from the web.
- mostly used to download software or automate file downloading in scripts
- supports recursive, interrupted downloads , authentication also



**`wget`** is optimized for downloading files and can be more efficient when downloading large files or entire websites.

```bash

wget http://example.com/file.zip = download this file with default name

wget -C http://example.com/file.zip = resume interrupted download

wget -r http://example.com = recursive download

wget --save-cookies cookies.txt http://example.com = save cookies

wget --ftp-user=username --ftp-password=password ftp://ftp.example.com/file.zip = with authentication for FTP

wget --user=username --password=password http://example.com/protected/file.zip = auth for http



wget --mirror -p --convert-links -P ./localdir http://example.com = mirror website 
-p = download all files like img, stylesheet for website 
--convert-links = converts link for local browsing
-P ./localdir = custom path to save




wget -O newname.zip http://example.com/file.zip = save with custom name

wget -i urls.txt = will download all files from url listed in urls.txt (one per line)

wget --limit-rate=100k http://example.com/largefile.zip = limit speed

wget -b http://example.com/largefile.zip = download in bg




```

