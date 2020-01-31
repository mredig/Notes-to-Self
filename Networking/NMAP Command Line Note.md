# NMAP Command Line Note

Ping Scan

* `nmap -sn 192.168.1.0/24` (scans entire range like 192.168.1.* )

Quick Scan

* `nmap -T4 -F 192.168.1.0/24`

Intense Scan

* `nmap -T4 -A -v 192.168.100.0/24`

Intense Plus UDP

* `nmap -sS -sU -T4 -A -v 192.168.100.0/24`

Regular Scan

* `nmap 192.168.1.0/24`
