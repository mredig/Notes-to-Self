<!-- permalink: f48a018b338eaaae84a1eb382e678ca1 DO NOT DELETE OR EDIT THIS LINE -->
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
