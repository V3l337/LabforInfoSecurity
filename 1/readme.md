# Task 1

1.

2. 
```
FTP
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523

SMTP
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566

HTTP
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750

PostgreSQL
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0224
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566
```

# Task 2
```
1. SYN "nmap -sS"
Этот тип сканирования отправляет SYN-пакет, который инициирует TCP-соединение. Если порт открыт, сервер ответит пакетом SYN/ACK. Если порт закрыт, сервер отправит RST

2. FIN "nmap -sF"
FIN-пакет отправляется для завершения TCP-соединения. Если порт закрыт, сервер ответит пакетом RST. Если порт открыт, сервер, скорее всего, не ответит

3. Xmas "nmap -sX"
В этом типе сканирования отправляются пакеты с установленными флагами FIN, PSH и URG. Подобно FIN-сканированию, открытые порты обычно не отвечают, тогда как закрытые отправляют RST

4. UDP "nmap -sU"
Этот тип сканирования отправляет UDP-пакеты на целевые порты. Если порт закрыт, сервер может отправить ICMP-сообщение типа "Port Unreachable". Открытые порты могут не ответить, так как UDP является бесконтактным протоколом
```


