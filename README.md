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

