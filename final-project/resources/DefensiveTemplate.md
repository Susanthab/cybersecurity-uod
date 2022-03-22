# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Kali 
  - **Operating System**: 5.4.0-kali3-amd64
  - **Purpose**: Attacking machine 
  - **IP Address**: 192.168.1.90
- ELK
  - **Operating System**: Ubuntu 18.04
  - **Purpose**: Hosting machine for the ELK stack
  - **IP Address**: 192.168.1.100
- Target 1
  - **Operating System**: Debian GNU/Linux 8
  - **Purpose**: The wordpress host
  - **IP Address**: 192.168.1.110
- Capstone
  - **Operating System**: Ubuntu 18.04
  - **Purpose**: The vulnerable web server
  - **IP Address**: 192.168.1.105

### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Name of Alert 1

Excessive HTTP Errors is implemented as follows:
  - **Metric**: WHEN count() GROUPED OVER top 5 'http.response.status_code'
  - **Threshold**: Is Above 400
  - **Vulnerability Mitigated**: Enumeration/Brute Force 
  - **Reliability**: The alert is highly reliable. Measuring by error codes 400 and above will filter out any normal or successful responses. 400+ codes are client and server errors which are of more concern. Especially when taking into account these error codes going off at a high rate.

#### Name of Alert 2
HTTP Request Size Monitor is implemented as follows:
  - **Metric**: WHEN sum() of http.request.bytes OVER all documents
  - **Threshold**: Is Above 3500
  - **Vulnerability Mitigated**: Code injection in HTTP requests (XSS and CRLF) or DDOS
  - **Reliability**: Alert could create false positives. It comes in at a medium reliability. There is a possibility for a large non malicious HTTP request or legitimate HTTP traffic.

#### Name of Alert 3
CPU Usage Monitor is implemented as follows:
  - **Metric**: system.process.cpu.total.pct
  - **Threshold**: Is Above 0.5
  - **Vulnerability Mitigated**: Malicious software, programs (malware or viruses) running taking up resources sepcially CPU
  - **Reliability**: The alert is highly reliable. Even if there isn’t a malicious program running this can still help determine where to improve on CPU usage.
