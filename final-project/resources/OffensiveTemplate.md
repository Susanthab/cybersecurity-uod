# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
_TODO: Fill out the information below._

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -sS -sV 192.168.1.0/24
```

![nmap-scan-1](/final-project/images/nmap-scan.png)
![nmap-scan-1](/final-project/images/nmap-scan-2.png)

This scan identifies the services below as potential points of entry:
- Target 1
  - port 22/tcp open ssh 
  - port 80/tcp open http
  - port 111/tcp open rcpbind
  - port 139/tcp open netbios-ssn
  - port 445/tcp open netbios-ssn

_TODO: Fill out the list below. Include severity, and CVE numbers, if possible._

The following vulnerabilities were identified on each target:
- Target 1
  - User enumeration (wordpress site)
  - Weak user password
  - Plain text password for MySQL database
  - Incorrect configuration of user privillages/privillage escalation using python

_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

Wordpress User Enumeration
![wordpress-enumerate.png](/final-project/images/wordpress-enumerate.png)

### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: flag1{b9bbcb33ellb80be759c4e844862482d}
    ![flag-1](/final-project/images/flag1.png)
    - **Exploit Used**
    Manual brute force attack to guess Michael's password. User password was weak and obvious. 
      - ssh michael@192.168.1.110
      - pw: michael (weak password)
      - cat /var/www/html/service.html (see above screenshot)
  - `flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a3e581c}
     ![flag-2](/final-project/images/flag2.png)
    - **Exploit Used**
    It was the same exploit used to get the flag1. 
      - ssh michael@192.168.1.110
      - pw: michael (weak password)
      - cat /var/www/flag2.txt
      -