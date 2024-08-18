# task 1

1. nmap -sA
```
root@VM1:~# nmap -sA 192.168.0.209
Starting Nmap 7.93 ( https://nmap.org ) at 2024-08-18 16:49 MSK
Nmap scan report for 192.168.0.209
Host is up (0.034s latency).
All 1000 scanned ports on 192.168.0.209 are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)
MAC Address: 0C:84:DC:5C:BE:4B (Hon Hai Precision Ind.)

Nmap done: 1 IP address (1 host up) scanned in 0.62 seconds

Ничего не повилось в журнале 
```
######Результаты показывают, что все порты на целевой машине находятся в игнорируемом состоянии. Это типично для сканирования ACK Scan, которое проверяет фильтрацию портов на основе ответов на ACK пакеты. Система защиты могла блокировать или не реагировать на эти пакеты, что не привело к записи в логи Suricata

2. nmap -sA
```
root@VM1:~# nmap -sT 192.168.0.209
Starting Nmap 7.93 ( https://nmap.org ) at 2024-08-18 16:50 MSK
Nmap scan report for 192.168.0.209
Host is up (0.0063s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 0C:84:DC:5C:BE:4B (Hon Hai Precision Ind.)

Nmap done: 1 IP address (1 host up) scanned in 0.29 seconds
```
```
8/18/2024-16:50:41.384231  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:52554 -> 192.168.0.209:3306
08/18/2024-16:50:41.384231  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:52554 -> 192.168.0.209:3306
08/18/2024-16:50:41.458074  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:33404 -> 192.168.0.209:5432
08/18/2024-16:50:41.458074  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:33404 -> 192.168.0.209:5432
08/18/2024-16:50:41.492403  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:35970 -> 192.168.0.209:1521
08/18/2024-16:50:41.492462  [**] [1:2002911:6] ET SCAN Potential VNC Scan 5900-5920 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:55434 -> 192.168.0.209:5911
08/18/2024-16:50:41.492403  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:35970 -> 192.168.0.209:1521
08/18/2024-16:50:41.492462  [**] [1:2002911:6] ET SCAN Potential VNC Scan 5900-5920 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:55434 -> 192.168.0.209:5911
08/18/2024-16:50:41.506757  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:35142 -> 192.168.0.209:1433
08/18/2024-16:50:41.506757  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:35142 -> 192.168.0.209:1433
08/18/2024-16:50:41.526791  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:56334 -> 192.168.0.209:5811
08/18/2024-16:50:41.526791  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:56334 -> 192.168.0.209:5811
```
######Логи показывают, что Suricata зафиксировала сканирование различных портов, несмотря на то, что фактически открыт только порт 22 SSH. Это может быть результатом настройки правил, которые отслеживают сканирование известных портов баз данных и сервисов (например, MySQL, MSSQL, Oracle SQL, VNC). Эти события могут быть результатом попыток проверки на наличие уязвимых сервисов

3. nmap -sA
```
root@VM1:~# nmap -sS 192.168.0.209
Starting Nmap 7.93 ( https://nmap.org ) at 2024-08-18 16:52 MSK
Nmap scan report for 192.168.0.209
Host is up (0.0054s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 0C:84:DC:5C:BE:4B (Hon Hai Precision Ind.)

Nmap done: 1 IP address (1 host up) scanned in 1.68 seconds
```
```
8/18/2024-16:52:05.728366  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:3306
08/18/2024-16:52:05.728366  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:3306
08/18/2024-16:52:05.760424  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:1521
08/18/2024-16:52:05.760424  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:1521
08/18/2024-16:52:05.823729  [**] [1:2002911:6] ET SCAN Potential VNC Scan 5900-5920 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5915
08/18/2024-16:52:05.823729  [**] [1:2002911:6] ET SCAN Potential VNC Scan 5900-5920 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5915
08/18/2024-16:52:05.910125  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:1433
08/18/2024-16:52:05.910125  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:1433
08/18/2024-16:52:05.996567  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5432
08/18/2024-16:52:05.996567  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5432
08/18/2024-16:52:06.126994  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5811
08/18/2024-16:52:06.126994  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:49252 -> 192.168.0.209:5811
```
######Suricata обнаружила сканирование портов, даже когда сканирование SYN Scan зафиксировало только открытый порт 22. Это подтверждает, что Suricata эффективно отслеживает попытки сканирования, даже если сканирование не обнаруживает открытых портов на целевой машине

4. nmap -sA
```
root@VM1:~# nmap -sV 192.168.0.209
Starting Nmap 7.93 ( https://nmap.org ) at 2024-08-18 16:52 MSK
Nmap scan report for 192.168.0.209
Host is up (0.0045s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.4 (Ubuntu Linux; protocol 2.0)
MAC Address: 0C:84:DC:5C:BE:4B (Hon Hai Precision Ind.)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.56 seconds
```
```
08/18/2024-16:52:47.775573  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:3306
08/18/2024-16:52:47.775573  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:3306
08/18/2024-16:52:47.854569  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:1433
08/18/2024-16:52:47.854993  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:5432
08/18/2024-16:52:47.854569  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:1433
08/18/2024-16:52:47.854993  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:5432
08/18/2024-16:52:47.906594  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:1521
08/18/2024-16:52:47.906594  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 192.168.0.10:63584 -> 192.168.0.209:1521
```
######Логи снова фиксируют попытки сканирования различных портов, несмотря на то, что на целевой машине открыт только порт 22. Это также подтверждает работу системы мониторинга, которая фиксирует попытки сканирования и потенциального поиска уязвимостей на известных сервисах

# task 2
















