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
###### Результаты показывают, что все порты на целевой машине находятся в игнорируемом состоянии. Это типично для сканирования ACK Scan, которое проверяет фильтрацию портов на основе ответов на ACK пакеты. Система защиты могла блокировать или не реагировать на эти пакеты, что не привело к записи в логи Suricata

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
###### Логи показывают, что Suricata зафиксировала сканирование различных портов, несмотря на то, что фактически открыт только порт 22 SSH. Это может быть результатом настройки правил, которые отслеживают сканирование известных портов баз данных и сервисов (например, MySQL, MSSQL, Oracle SQL, VNC). Эти события могут быть результатом попыток проверки на наличие уязвимых сервисов

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
###### Suricata обнаружила сканирование портов, даже когда сканирование SYN Scan зафиксировало только открытый порт 22. Это подтверждает, что Suricata эффективно отслеживает попытки сканирования, даже если сканирование не обнаруживает открытых портов на целевой машине

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
###### Логи снова фиксируют попытки сканирования различных портов, несмотря на то, что на целевой машине открыт только порт 22. Это также подтверждает работу системы мониторинга, которая фиксирует попытки сканирования и потенциального поиска уязвимостей на известных сервисах

# task 2
1. Вывод журнала Suricata
```
08/18/2024-17:14:27.374629  [**] [1:2001219:20] ET SCAN Potential SSH Scan [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45380 -> 192.168.0.209:22
08/18/2024-17:14:27.374629  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45380 -> 192.168.0.209:22
08/18/2024-17:14:27.374629  [**] [1:2001219:20] ET SCAN Potential SSH Scan [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45380 -> 192.168.0.209:22
08/18/2024-17:14:27.374629  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45380 -> 192.168.0.209:22
08/18/2024-17:14:27.375724  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45358 -> 192.168.0.209:22
08/18/2024-17:14:27.375860  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45336 -> 192.168.0.209:22
08/18/2024-17:14:27.375724  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45358 -> 192.168.0.209:22
08/18/2024-17:14:27.375943  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:45408 -> 192.168.0.209:22
08/18/2024-17:14:29.589515  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42580 -> 192.168.0.209:22
08/18/2024-17:14:29.589515  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42580 -> 192.168.0.209:22
08/18/2024-17:14:29.593787  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42582
08/18/2024-17:14:29.593787  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42582
08/18/2024-17:14:29.600679  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42602
08/18/2024-17:14:29.600679  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42602
08/18/2024-17:14:29.644151  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42624 -> 192.168.0.209:22
08/18/2024-17:14:29.644151  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42624 -> 192.168.0.209:22
08/18/2024-17:14:29.648209  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42624
08/18/2024-17:14:29.648209  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42624
08/18/2024-17:14:29.701431  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42676 -> 192.168.0.209:22
08/18/2024-17:14:29.701431  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42676 -> 192.168.0.209:22
08/18/2024-17:14:29.708050  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:42678 -> 192.168.0.209:22
08/18/2024-17:14:29.708050  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:42678 -> 192.168.0.209:22
08/18/2024-17:14:29.709552  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42674
08/18/2024-17:14:29.709552  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42674
08/18/2024-17:14:29.710395  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42680
08/18/2024-17:14:29.710395  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42680
08/18/2024-17:14:29.714025  [**] [1:2006546:9] ET SCAN LibSSH Based Frequent SSH Connections Likely BruteForce Attack [**] [Classification: Attempted Administrator Privilege Gain] [Priority: 1] {TCP} 192.168.0.10:42674 -> 192.168.0.209:22
08/18/2024-17:14:29.714025  [**] [1:2006546:9] ET SCAN LibSSH Based Frequent SSH Connections Likely BruteForce Attack [**] [Classification: Attempted Administrator Privilege Gain] [Priority: 1] {TCP} 192.168.0.10:42674 -> 192.168.0.209:22
08/18/2024-17:14:29.718089  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42704
08/18/2024-17:14:29.718089  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42704
08/18/2024-17:14:29.722379  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42708 -> 192.168.0.209:22
08/18/2024-17:14:29.722379  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42708 -> 192.168.0.209:22
08/18/2024-17:14:29.724919  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42708
08/18/2024-17:14:29.724919  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42708
08/18/2024-17:14:29.731038  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:42710 -> 192.168.0.209:22
08/18/2024-17:14:29.731038  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:42710 -> 192.168.0.209:22
08/18/2024-17:14:29.747267  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42752 -> 192.168.0.209:22
08/18/2024-17:14:29.747267  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42752 -> 192.168.0.209:22
08/18/2024-17:14:29.759125  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42752
08/18/2024-17:14:29.759125  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42752
08/18/2024-17:14:29.760335  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42782
08/18/2024-17:14:29.760335  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42782
08/18/2024-17:14:29.802410  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42800
08/18/2024-17:14:29.802410  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42800
08/18/2024-17:14:29.809905  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42816 -> 192.168.0.209:22
08/18/2024-17:14:29.809905  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42816 -> 192.168.0.209:22
08/18/2024-17:14:32.698195  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42868 -> 192.168.0.209:22
08/18/2024-17:14:32.698195  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42868 -> 192.168.0.209:22
08/18/2024-17:14:32.817696  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42900
08/18/2024-17:14:32.817696  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42900
08/18/2024-17:14:32.838372  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42916 -> 192.168.0.209:22
08/18/2024-17:14:32.838372  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42916 -> 192.168.0.209:22
08/18/2024-17:14:32.847384  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42916
08/18/2024-17:14:32.847384  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42916
08/18/2024-17:14:32.949168  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42922
08/18/2024-17:14:32.949168  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42922
08/18/2024-17:14:33.066350  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42958
08/18/2024-17:14:33.066350  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:42958
08/18/2024-17:14:33.073551  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42966 -> 192.168.0.209:22
08/18/2024-17:14:33.073551  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:42966 -> 192.168.0.209:22
08/18/2024-17:14:33.917932  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43012 -> 192.168.0.209:22
08/18/2024-17:14:33.917932  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43012 -> 192.168.0.209:22
08/18/2024-17:14:33.980693  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43018
08/18/2024-17:14:33.980693  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43018
08/18/2024-17:14:34.687183  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.142:25317 -> 192.168.0.209:22
08/18/2024-17:14:36.045024  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43050 -> 192.168.0.209:22
08/18/2024-17:14:36.044977  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43052 -> 192.168.0.209:22
08/18/2024-17:14:36.047213  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43052
08/18/2024-17:14:36.047213  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43052
08/18/2024-17:14:36.047873  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43050
08/18/2024-17:14:36.047873  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43050
08/18/2024-17:14:36.101073  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43078
08/18/2024-17:14:36.101073  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43078
08/18/2024-17:14:36.101155  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43076
08/18/2024-17:14:36.101155  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43076
08/18/2024-17:14:36.121142  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43104 -> 192.168.0.209:22
08/18/2024-17:14:36.121142  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43104 -> 192.168.0.209:22
08/18/2024-17:14:36.125225  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:43116 -> 192.168.0.209:22
08/18/2024-17:14:36.125225  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.10:43116 -> 192.168.0.209:22
08/18/2024-17:14:36.132192  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43120
08/18/2024-17:14:36.132192  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43120
08/18/2024-17:14:36.132803  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43124
08/18/2024-17:14:36.132803  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43124
08/18/2024-17:14:36.148637  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43152 -> 192.168.0.209:22
08/18/2024-17:14:36.148637  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43152 -> 192.168.0.209:22
08/18/2024-17:14:36.151023  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43152
08/18/2024-17:14:36.151023  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43152
08/18/2024-17:14:37.317000  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43184
08/18/2024-17:14:37.317000  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43184
08/18/2024-17:14:37.342657  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43188 -> 192.168.0.209:22
08/18/2024-17:14:37.342657  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43188 -> 192.168.0.209:22
08/18/2024-17:14:37.350051  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43190
08/18/2024-17:14:37.350051  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43190
08/18/2024-17:14:37.501733  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43228 -> 192.168.0.209:22
08/18/2024-17:14:37.501733  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:43228 -> 192.168.0.209:22
08/18/2024-17:14:37.505116  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43228
08/18/2024-17:14:37.505116  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:43228
08/18/2024-17:14:39.262077  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:60800 -> 192.168.0.209:22
08/18/2024-17:14:39.262077  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.0.10:60800 -> 192.168.0.209:22
08/18/2024-17:14:39.350145  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:60816
08/18/2024-17:14:39.350145  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:60816
08/18/2024-17:14:39.371333  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:60826
08/18/2024-17:14:39.371333  [**] [1:2260002:1] SURICATA Applayer Detect protocol only one direction [**] [Classification: Generic Protocol Command Decode] [Priority: 3] {TCP} 192.168.0.209:22 -> 192.168.0.10:60826
```
2. Вывод журнала fail2ban
```
024-08-18 17:18:15,623 fail2ban.server         [18372]: INFO    --------------------------------------------------
2024-08-18 17:18:15,623 fail2ban.server         [18372]: INFO    Starting Fail2ban v1.0.2
2024-08-18 17:18:15,624 fail2ban.observer       [18372]: INFO    Observer start...
2024-08-18 17:18:15,632 fail2ban.database       [18372]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2024-08-18 17:18:15,633 fail2ban.jail           [18372]: INFO    Creating new jail 'sshd'
2024-08-18 17:18:15,794 fail2ban.jail           [18372]: INFO    Jail 'sshd' uses systemd {}
2024-08-18 17:18:15,795 fail2ban.jail           [18372]: INFO    Initiated 'systemd' backend
2024-08-18 17:18:15,796 fail2ban.filter         [18372]: INFO      maxLines: 1
2024-08-18 17:18:15,821 fail2ban.filtersystemd  [18372]: INFO    [sshd] Added journal match for: '_SYSTEMD_UNIT=sshd.service + _COMM=sshd'
2024-08-18 17:18:15,821 fail2ban.filter         [18372]: INFO      maxRetry: 5
2024-08-18 17:18:15,821 fail2ban.filter         [18372]: INFO      findtime: 600
2024-08-18 17:18:15,822 fail2ban.actions        [18372]: INFO      banTime: 600
2024-08-18 17:18:15,822 fail2ban.filter         [18372]: INFO      encoding: UTF-8
2024-08-18 17:18:15,823 fail2ban.jail           [18372]: INFO    Jail 'sshd' started
2024-08-18 17:18:15,841 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:26
2024-08-18 17:18:15,843 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,844 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,844 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,845 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,845 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,846 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,847 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,847 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,848 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,848 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,849 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,849 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,850 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,851 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,851 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,852 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,855 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,860 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:27
2024-08-18 17:18:15,861 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,862 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,863 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,863 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,864 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,864 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,865 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,865 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,866 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,866 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,867 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,867 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,868 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,868 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,869 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,869 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,870 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,872 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,873 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,878 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,879 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,879 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,881 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:29
2024-08-18 17:18:15,883 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,884 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,884 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,885 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,885 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,886 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,886 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,887 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,888 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,889 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,889 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,890 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,890 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:31
2024-08-18 17:18:15,891 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:32
2024-08-18 17:18:15,899 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:33
2024-08-18 17:18:15,899 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:33
2024-08-18 17:18:15,901 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,902 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,902 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,903 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,903 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,904 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,904 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,905 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,905 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,906 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,906 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,907 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:35
2024-08-18 17:18:15,907 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:36
2024-08-18 17:18:15,910 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:36
2024-08-18 17:18:15,912 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:36
2024-08-18 17:18:15,914 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:37
2024-08-18 17:18:15,918 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,919 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,919 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,920 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,920 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,921 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:38
2024-08-18 17:18:15,925 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,925 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,926 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,926 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,927 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,927 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:39
2024-08-18 17:18:15,929 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:40
2024-08-18 17:18:15,930 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:40
2024-08-18 17:18:15,930 fail2ban.filter         [18372]: INFO    [sshd] Found 192.168.0.10 - 2024-08-18 17:14:41
2024-08-18 17:18:15,944 fail2ban.filtersystemd  [18372]: INFO    [sshd] Jail is in operation now (process new journal entries)
2024-08-18 17:18:16,023 fail2ban.actions        [18372]: NOTICE  [sshd] Ban 192.168.0.10
2024-08-18 17:18:16,214 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,224 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,224 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
2024-08-18 17:18:16,225 fail2ban.actions        [18372]: NOTICE  [sshd] 192.168.0.10 already banned
```

##### Suricata обнаружела попытки сканирования 22 SSH порта. ET SCAN LibSSH Based Frequent SSH Connections Likely BruteForce Attack - указывают на возможные попытки атаки методом перебора паролей через SSH. Это подтверждается частыми попытками подключения к порту 22 с различными исходящими портами. [Priority: 1] - дал высокий приоритет этим событиям. SURICATA Applayer Detect protocol only one direction - указывает на проблемы с обнаружением протокола в одном направлении, может быть связано с неудачными попытками установить соединение или неправильно настроенным сетевым оборудованием. Логи показывают множество событий, происходящих в течение короткого промежутка времени.

##### fail2ban (17:18:15,841 до 17:18:15,930:) Множественные записи в журнале показывают, что Fail2ban обнаружил многочисленные неудачные попытки входа с IP-адреса 192.168.0.10 . 17:18:16,023: Fail2ban блокирует IP-адрес 192.168.0.10 . 17:18:16,214 до 17:18:16,225: В журнале многократно показывается, что IP-адрес 192.168.0.10 уже заблокирован. Это указывает на то, что тот же IP пытался взломать систему несколько раз, и блокировка была применена.
