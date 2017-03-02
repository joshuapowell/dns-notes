# DNS Notes
Notes on discovering DNS information.

## Lookup Domain Zone File or "All DNS Records"

### Using `dig` on macOS

#### Discovering DNS Information

To display A, AAAA, NS, MX, SOA, and TXT DNS records with their Record name, TTY, Record Type, and Record Value, execute this command at the macOS Terminal propmt:

```
dig -t ANY viableindustries.com
```

You should receive a response in the following format. Your mileage will vary based on DNS host factors.

```
; <<>> DiG 9.8.3-P1 <<>> -t ANY viableindustries.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39210
;; flags: qr rd ra; QUERY: 1, ANSWER: 12, AUTHORITY: 0, ADDITIONAL: 4

;; QUESTION SECTION:
;viableindustries.com.		IN	ANY

;; ANSWER SECTION:
viableindustries.com.	300	IN	TXT	"v=spf1 include:spf.mandrillapp.com ?all"
viableindustries.com.	172800	IN	NS	ns-1450.awsdns-53.org.
viableindustries.com.	172800	IN	NS	ns-1836.awsdns-37.co.uk.
viableindustries.com.	172800	IN	NS	ns-29.awsdns-03.com.
viableindustries.com.	172800	IN	NS	ns-711.awsdns-24.net.
viableindustries.com.	900	IN	SOA	ns-711.awsdns-24.net. awsdns-hostmaster.amazon.com. 1 7200 900 1209600 86400
viableindustries.com.	300	IN	A	107.170.129.166
viableindustries.com.	300	IN	MX	30 aspmx2.googlemail.com.
viableindustries.com.	300	IN	MX	30 aspmx3.googlemail.com.
viableindustries.com.	300	IN	MX	10 aspmx.l.google.com.
viableindustries.com.	300	IN	MX	20 alt1.aspmx.l.google.com.
viableindustries.com.	300	IN	MX	20 alt2.aspmx.l.google.com.

;; ADDITIONAL SECTION:
ns-1450.awsdns-53.org.	160844	IN	A	205.251.197.170
ns-1836.awsdns-37.co.uk. 160760	IN	A	205.251.199.44
ns-1836.awsdns-37.co.uk. 170135	IN	AAAA	2600:9000:5307:2c00::1
ns-29.awsdns-03.com.	79866	IN	A	205.251.192.29

;; Query time: 57 msec
;; SERVER: 2001:558:feed::2#53(2001:558:feed::2)
;; WHEN: Thu Mar  2 09:39:45 2017
;; MSG SIZE  rcvd: 509
```

#### Reference

```
Usage:  dig [@global-server] [domain] [q-type] [q-class] {q-opt}
            {global-d-opt} host [@local-server] {local-d-opt}
            [ host [@local-server] {local-d-opt} [...]]
Where:  domain	  is in the Domain Name System
        q-class  is one of (in,hs,ch,...) [default: in]
        q-type   is one of (a,any,mx,ns,soa,hinfo,axfr,txt,...) [default:a]
                 (Use ixfr=version for type ixfr)
        q-opt    is one of:
                 -x dot-notation     (shortcut for reverse lookups)
                 -i                  (use IP6.INT for IPv6 reverse lookups)
                 -f filename         (batch mode)
                 -b address[#port]   (bind to source address/port)
                 -p port             (specify port number)
                 -q name             (specify query name)
                 -t type             (specify query type)
                 -c class            (specify query class)
                 -k keyfile          (specify tsig key file)
                 -y [hmac:]name:key  (specify named base64 tsig key)
                 -4                  (use IPv4 query transport only)
                 -6                  (use IPv6 query transport only)
                 -m                  (enable memory usage debugging)
        d-opt    is of the form +keyword[=value], where keyword is:
                 +[no]vc             (TCP mode)
                 +[no]tcp            (TCP mode, alternate syntax)
                 +time=###           (Set query timeout) [5]
                 +tries=###          (Set number of UDP attempts) [3]
                 +retry=###          (Set number of UDP retries) [2]
                 +domain=###         (Set default domainname)
                 +bufsize=###        (Set EDNS0 Max UDP packet size)
                 +ndots=###          (Set NDOTS value)
                 +edns=###           (Set EDNS version)
                 +[no]search         (Set whether to use searchlist)
                 +[no]showsearch     (Search with intermediate results)
                 +[no]defname        (Ditto)
                 +[no]recurse        (Recursive mode)
                 +[no]ignore         (Don't revert to TCP for TC responses.)
                 +[no]fail           (Don't try next server on SERVFAIL)
                 +[no]besteffort     (Try to parse even illegal messages)
                 +[no]aaonly         (Set AA flag in query (+[no]aaflag))
                 +[no]adflag         (Set AD flag in query)
                 +[no]cdflag         (Set CD flag in query)
                 +[no]cl             (Control display of class in records)
                 +[no]cmd            (Control display of command line)
                 +[no]comments       (Control display of comment lines)
                 +[no]question       (Control display of question)
                 +[no]answer         (Control display of answer)
                 +[no]authority      (Control display of authority)
                 +[no]additional     (Control display of additional)
                 +[no]stats          (Control display of statistics)
                 +[no]short          (Disable everything except short
                                      form of answer)
                 +[no]ttlid          (Control display of ttls in records)
                 +[no]all            (Set or clear all display flags)
                 +[no]qr             (Print question before sending)
                 +[no]nssearch       (Search all authoritative nameservers)
                 +[no]identify       (ID responders in short answers)
                 +[no]trace          (Trace delegation down from root)
                 +[no]dnssec         (Request DNSSEC records)
                 +[no]nsid           (Request Name Server ID)
                 +[no]multiline      (Print records in an expanded format)
                 +[no]onesoa         (AXFR prints only one soa record)
        global d-opts and servers (before host name) affect all queries.
        local d-opts and servers (after host name) affect only that lookup.
        -h                           (print help and exit)
        -v                           (print version and exit)
```
