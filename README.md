# 3.6_1

# 1
Получил код 301 от сервера, который говорит, что запрашиваемая страница `http://stackoverflow.com/questions` постоянно перемещена на `https://stackoverflow.com/questions`
```
vagrant@vagrant:~$ telnet stackoverflow.com 80
Trying 151.101.1.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: de0ed408-8485-4ae1-9b06-20d44abb4963
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Sun, 13 Feb 2022 13:13:33 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-fra19134-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1644758014.826438,VS0,VE85
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=263d086b-1676-f32d-7e8e-b80c56700a1b; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
# 2
Первый ответ с кодом 307 (Internal Redirect)  
Больше всех загружался сам документ stackoverflow.com
![image](https://user-images.githubusercontent.com/97126500/153756173-a67c8a54-4e2a-4841-b28b-d7c462505be4.png)
# 3
```
vagrant@vagrant:~$ curl ifconfig.me/ip
78.37.255.185
```
# 4
ROSTELECOM, AS12389
```
vagrant@vagrant:~$ whois 78.37.255.185
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '78.37.192.0 - 78.37.255.255'

% Abuse contact for '78.37.192.0 - 78.37.255.255' is 'abuse@rt.ru'

inetnum:        78.37.192.0 - 78.37.255.255
netname:        RU-AVANGARD-DSL
descr:          "St.Petersburg Telephone Network"
descr:          branch of the JSC "North-West Telecom"
descr:          24,Bolshaya Morskaya str.191186 St-Petersburg,Russia
country:        RU
admin-c:        RCR3-RIPE
tech-c:         RCR3-RIPE
status:         ASSIGNED PA
mnt-by:         AS8997-MNT
mnt-lower:      AS8997-MNT
created:        2009-12-10T16:51:39Z
last-modified:  2009-12-10T16:51:39Z
source:         RIPE

role:           ru.spbnit contact role
address:        OJSC Rostelecom
address:        Macro-regional branch Northwest
address:        14/26 Gorokhovaya str. (26 Bolshaya Morskaya str.)
address:        191186, St.-Petersburg
address:        Russia
phone:          +7 812 595 45 56
remarks:        --------------------------------------------
admin-c:        AA728-RIPE
admin-c:        VE128-RIPE
tech-c:         AA728-RIPE
tech-c:         VE128-RIPE
tech-c:         TR4627-RIPE
nic-hdl:        RCR3-RIPE
remarks:        --------------------------------------------
remarks:        Spam & Abuse: abuse(at)dtd.ptn.ru
remarks:        General questions: ip-noc(at)nw.rt.ru
remarks:        Routing & peering: ip-noc(at)nw.rt.ru
remarks:        --------------------------------------------
abuse-mailbox:  abuse@dtd.ptn.ru
mnt-by:         AS8997-MNT
created:        2002-09-04T09:29:24Z
last-modified:  2022-02-08T10:51:49Z
source:         RIPE # Filtered

% Information related to '78.37.128.0/17AS12389'

route:          78.37.128.0/17
descr:          Rostelecom networks
origin:         AS12389
mnt-by:         ROSTELECOM-MNT
created:        2018-10-31T12:34:26Z
last-modified:  2018-10-31T12:34:26Z
source:         RIPE # Filtered

% This query was served by the RIPE Database Query Service version 1.102.2 (BLAARKOP)

```
# 5
Сети:  
92.101.243.1  
212.48.194.242  
188.254.2.4  
87.226.194.47  
74.125.244.132  
72.14.232.85  
142.251.51.187  
209.85.254.179  
AS:  
AS12389  
AS15169  
```
vagrant@vagrant:~$ traceroute -IAn 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  10.0.2.2 [*]  1.263 ms  1.133 ms  1.039 ms
 2  * * *
 3  92.101.243.1 [AS12389]  13.608 ms  14.143 ms  13.921 ms
 4  212.48.194.242 [AS12389]  14.742 ms  15.328 ms  15.125 ms
 5  188.254.2.4 [AS12389]  15.029 ms  14.846 ms  16.812 ms
 6  87.226.194.47 [AS12389]  14.613 ms  16.059 ms  15.616 ms
 7  74.125.244.132 [AS15169]  15.378 ms  9.824 ms  9.610 ms
 8  72.14.232.85 [AS15169]  13.209 ms  13.040 ms  12.867 ms
 9  142.251.51.187 [AS15169]  13.999 ms * *
10  209.85.254.179 [AS15169]  11.483 ms  12.612 ms  12.441 ms
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  8.8.8.8 [AS15169]  14.330 ms  14.266 ms  14.181 ms
```
# 6
Наибольшая задержка между 72.14.232.85 и 142.251.51.187
![image](https://user-images.githubusercontent.com/97126500/153758415-dcf69144-42ff-40c1-ab22-61b8be86f5dc.png)
# 7
ns1.zdns.google.  
ns3.zdns.google.  
ns2.zdns.google.  
ns4.zdns.google.  
```
vagrant@vagrant:~$ dig dns.google NS

; <<>> DiG 9.16.1-Ubuntu <<>> dns.google NS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22925
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;dns.google.                    IN      NS

;; ANSWER SECTION:
dns.google.             14400   IN      NS      ns1.zdns.google.
dns.google.             14400   IN      NS      ns3.zdns.google.
dns.google.             14400   IN      NS      ns2.zdns.google.
dns.google.             14400   IN      NS      ns4.zdns.google.

;; Query time: 24 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Feb 13 14:52:10 UTC 2022
;; MSG SIZE  rcvd: 116
```
IP адреса 8.8.8.8 и 8.8.4.4  
```
vagrant@vagrant:~$ dig dns.google A

; <<>> DiG 9.16.1-Ubuntu <<>> dns.google A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50603
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;dns.google.                    IN      A

;; ANSWER SECTION:
dns.google.             524     IN      A       8.8.8.8
dns.google.             524     IN      A       8.8.4.4

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Feb 13 14:56:00 UTC 2022
;; MSG SIZE  rcvd: 71

vagrant@vagrant:~$
```
# 8
dns.google.  
```
vagrant@vagrant:~$ dig -x 8.8.8.8

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27152
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   7111    IN      PTR     dns.google.

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Feb 13 15:01:49 UTC 2022
;; MSG SIZE  rcvd: 73

vagrant@vagrant:~$ dig -x 8.8.4.4

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29566
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   7096    IN      PTR     dns.google.

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Feb 13 15:02:50 UTC 2022
;; MSG SIZE  rcvd: 73
```
