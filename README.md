# LAB 1 – NETWORK & SERVICE RECONNAISSANCE WITH METASPLOITABLE 2
LAB 1 – NETWORK &amp; SERVICE RECONNAISSANCE WITH METASPLOITABLE 2 EVIDENCE REPORT
# ICDFA | WADF - 2026-M02 | Cybersecurity Practical Lab

**Submission Date:** 6th SEPTEMBER, 2026

---

## Student Identification Details

| **Student Identification Details** | **Information**                     |
| ---------------------------------- | ----------------------------------- |
| **Full Name**                      | OMOWUMI SHARON                      |
| **Registration Number**            | FDFC2617050                         |
| **Linux Distribution / Version**   | KALI DEBIAN LINUX                   |
| **VM Hostname**                    | Sharonkali-lab                      |
| **Lab Target**                     | Metasploitable 2 – `192.168.56.102` |

---

# 1. Lab Overview

## Objective

The objective of this practical lab was to perform **network and service reconnaissance** against an intentionally vulnerable Metasploitable 2 virtual machine in an isolated and authorized laboratory environment.

The assessment focused on identifying:

* The target host and network connectivity
* Open TCP and UDP ports
* Running network services
* Service versions
* Operating system information
* NSE-based service enumeration
* HTTP server information
* SMB information
* SSH host keys
* FTP configuration
* Web technologies using WhatWeb

The reconnaissance results were used to create a service inventory and understand the information that can be gathered from a target before vulnerability assessment.

> **Authorization Notice:** All scanning and enumeration in this report were performed against the intentionally vulnerable Metasploitable 2 laboratory machine at `192.168.56.102`.

---

# 2. Lab Environment

| **Component**           | **Details**                  |
| ----------------------- | ---------------------------- |
| Attacker Machine        | Kali Linux                   |
| Kali Hostname           | `Sharonkali-lab`             |
| Target Machine          | Metasploitable 2             |
| Target IP               | `192.168.56.102`             |
| Network Type            | Isolated Virtual Lab Network |
| Primary Tool            | Nmap                         |
| Web Fingerprinting Tool | WhatWeb                      |
| HTTP Utility            | curl                         |

---

# 3. Tools Used

| **Tool / Command** | **Purpose**                                       |
| ------------------ | ------------------------------------------------- |
| `ip addr`          | Identify the Kali machine's network configuration |
| `ifconfig`         | Identify the Metasploitable network configuration |
| `ping`             | Test network connectivity                         |
| `nmap`             | Perform host discovery and port/service scanning  |
| Nmap NSE           | Perform additional service enumeration            |
| `curl`             | Retrieve HTTP response headers                    |
| `whatweb`          | Identify web technologies and applications        |

---

# 4. Part 1 – Preparing the Lab

## Steps 1–3: Network Configuration and Connectivity

### Commands

```bash
ip addr
```

```bash
ifconfig
```

```bash
ping -c 4 192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot A lab 1" src="https://github.com/user-attachments/assets/7fb422cc-727e-4694-b158-eaae3e6df4bd" />

**Screenshot 1-1: Lab 1 – Network Configuration, Target Identification and Connectivity**

### Explanation

| **Command**                | **Purpose**                                         | **Expected / Observed Result**               |
| -------------------------- | --------------------------------------------------- | -------------------------------------------- |
| `ip addr`                  | Displays Kali's network interfaces and IP addresses | Identifies the Kali VM network configuration |
| `ifconfig`                 | Displays the target's network interface information | Identifies the Metasploitable IP address     |
| `ping -c 4 192.168.56.102` | Tests communication with the target                 | Successful replies confirm connectivity      |

---

# 5. Part 3 – Core Nmap Scanning

## Steps 4–6: Host Discovery, Default Scan and Service Detection

### Commands

```bash
nmap -sn 192.168.56.102
```

```bash
nmap 192.168.56.102
```

```bash
nmap -sV 192.168.56.102
```

### Screenshot Evidence

<img width="1920" height="1003" alt="screenshot B lab 1" src="https://github.com/user-attachments/assets/b2b9d6d0-36ff-40f3-abc6-010e1e05123a" />


**Screenshot 2-1: Lab 1 – Host Discovery, Default TCP Scan and Service Version Detection**

### Explanation

| **Command** | **Purpose**                                            |
| ----------- | ------------------------------------------------------ |
| `nmap -sn`  | Performs host discovery without conducting a port scan |
| `nmap`      | Performs Nmap's default TCP port scan                  |
| `nmap -sV`  | Attempts to identify service names and versions        |

---

## Steps 7–9: Version Intensity, OS Detection and Aggressive Scanning

### Commands

```bash
nmap -sV --version-intensity 9 192.168.56.102
```

```bash
sudo nmap -O 192.168.56.102
```

```bash
sudo nmap -A 192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot C lab 1" src="https://github.com/user-attachments/assets/03396854-7673-4dd9-be52-7a3568f3414f" />

**Screenshot 3-1: Lab 1 – Service Version Intensity, OS Detection and Aggressive Enumeration**

### Results – Step 8

The OS detection scan identified the target as:

* General-purpose device
* Linux operating system
* Linux kernel in the `2.6.x` family
* OS range approximately `Linux 2.6.9–2.6.33`
* Network distance: 1 hop
* Virtual NIC identified as Oracle VirtualBox

### Results – Step 9

The aggressive scan identified numerous services, including:

* FTP – vsftpd 2.3.4
* SSH – OpenSSH 4.7p1
* Telnet
* SMTP – Postfix
* DNS – ISC BIND 9.4.2
* HTTP – Apache 2.2.8
* SMB – Samba
* MySQL 5.0.51a
* PostgreSQL 8.3.x
* VNC
* UnrealIRCd
* Apache Tomcat 5.5

Additional information included an anonymous FTP login, HTTP title information, SMB/NetBIOS information and operating-system fingerprints.

### Explanation

| **Command**                 | **Purpose**                                  | **Result / Finding**                                             |
| --------------------------- | -------------------------------------------- | ---------------------------------------------------------------- |
| `-sV --version-intensity 9` | Performs intensive service version detection | Provides detailed service fingerprinting                         |
| `-O`                        | Attempts operating system detection          | Identified Linux 2.6.x                                           |
| `-A`                        | Enables several advanced detection features  | Identified OS, services, scripts and additional host information |

---

# 6. Full TCP Port Scanning

## Steps 10–12: Full TCP Range and Timing

### Commands

```bash
sudo nmap -p- 192.168.56.102
```

```bash
sudo nmap -p- -sV 192.168.56.102
```

```bash
sudo nmap -p- -T4 192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot D lab 1" src="https://github.com/user-attachments/assets/ec45df22-ece9-4b23-b924-48adac106d02" />

**Screenshot 4-1: Lab 1 – Full TCP Port and Service Enumeration**

### Results

The full TCP scan identified **30 open TCP ports** on the target.

The `-p-` option scans ports 1 through 65535 instead of only the common/default port set.

The `-p- -sV` scan provided service version information for the discovered ports.

The `-T4` scan applied Nmap's aggressive timing template. In this lab environment, the T4 scan was not necessarily faster than the previous full scan because scan speed can vary depending on the virtual network and target response behaviour.

### Explanation

| **Command** | **Purpose**                                            |
| ----------- | ------------------------------------------------------ |
| `-p-`       | Scans all TCP ports from 1–65535                       |
| `-p- -sV`   | Scans all TCP ports and identifies service versions    |
| `-p- -T4`   | Performs a full TCP scan using Nmap timing template T4 |

---

# 7. Selected Port and Port Range Scanning

## Steps 13–15: Selected TCP Ports, Ports 1–1024 and UDP

### Commands

```bash
nmap -p 21,22,23,25,80,139,445 192.168.56.102
```

```bash
nmap -p 1-1024 192.168.56.102
```

```bash
sudo nmap -sU 192.168.56.102
```

### Screenshot Evidence

<img width="1920" height="1003" alt="screenshot E lab 1" src="https://github.com/user-attachments/assets/e4fb798c-c9ed-4a85-8b30-9becdb976d3c" />

**Screenshot 5-1: Lab 1 – Selected TCP Ports, TCP Range and UDP Enumeration**

### Results – Step 13

The selected scan identified all seven requested ports as open:

* 21 – FTP
* 22 – SSH
* 23 – Telnet
* 25 – SMTP
* 80 – HTTP
* 139 – NetBIOS/SMB
* 445 – Microsoft-DS/SMB

### Results – Step 14

The scan of ports `1–1024` identified 12 open ports, including:

* 21
* 22
* 23
* 25
* 53
* 80
* 111
* 139
* 445
* 512
* 513
* 514

### Results – Step 15

The full UDP scan took approximately **17 minutes 15 seconds**.

Important UDP results included:

| **Port** | **State**     | **Service**          |
| -------- | ------------- | -------------------- |
| 53       | Open          | DNS                  |
| 68       | Open/Filtered | DHCP client          |
| 69       | Open/Filtered | TFTP                 |
| 111      | Open          | RPCBind              |
| 137      | Open          | NetBIOS Name Service |
| 138      | Open/Filtered | NetBIOS Datagram     |
| 2049     | Open          | NFS                  |

### Explanation

UDP scanning is generally slower than TCP scanning because UDP is connectionless and many services do not return a response to probes. Nmap may therefore need to wait for timeout responses before determining the state.

---

# 8. Top UDP Ports

## Steps 16–18: Top 20 UDP Ports, NSE and HTTP Title

### Commands

```bash
sudo nmap -sU --top-ports 20 -sV 192.168.56.102
```

```bash
nmap -sC -sV 192.168.56.102
```

```bash
nmap --script http-title -p 80,8180 192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot F1 lab 1" src="https://github.com/user-attachments/assets/2500f3c3-7441-48f2-bde1-0b36b2252b0c" />
<img width="1920" height="1003" alt="screenshot F2 lab 1" src="https://github.com/user-attachments/assets/43588eab-6217-438b-b257-79256a93b4f5" />


**Screenshot 6-1: Lab 1 – Top UDP Ports, Default NSE Scripts and HTTP Title Enumeration**

### Results – Step 16

The top-20 UDP scan completed in approximately **112 seconds**, substantially faster than the full UDP scan.

Important results included:

* `53/udp` – DNS, ISC BIND 9.4.2
* `137/udp` – NetBIOS Name Service
* `67/udp` – DHCP
* `68/udp` – DHCP client
* `69/udp` – TFTP
* `123/udp` – NTP
* `161/udp` – SNMP
* `162/udp` – SNMP Trap
* `445/udp` – Microsoft-DS

Some UDP states were reported as `open|filtered`, meaning Nmap could not conclusively distinguish an open service from packet filtering.

> **Note:** The service-probe metadata for some UDP ports produced an inconsistent Windows-related OS/service description. The stronger OS evidence from TCP scans identified the target as Linux/Unix, so the UDP metadata was treated cautiously rather than as a definitive OS identification.

### Results – Step 17

The default NSE/service scan produced several useful findings:

* Anonymous FTP login allowed
* SSH host keys identified
* HTTP server and title identified
* SMB/NetBIOS information identified
* SMB signing reported as disabled
* MySQL information identified
* RPC/NFS information identified

### Results – Step 18

The HTTP title enumeration was used to identify the title of the web services exposed on ports 80 and 8180.

---

# 9. HTTP, SMB and SSH Enumeration

## Steps 19–21

### Commands

```bash
nmap --script http-headers -p 80,8180 192.168.56.102
```

```bash
nmap --script smb-protocols -p 139,445 192.168.56.102
```

```bash
nmap --script ssh-hostkey -p 22 192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot G lab 1" src="https://github.com/user-attachments/assets/bedc862f-c7cf-4fba-b684-21b4366d0e93" />


**Screenshot 7-1: Lab 1 – HTTP Headers, SMB Protocols and SSH Host Key Enumeration**

### Explanation

| **NSE Script**  | **Purpose**                                         |
| --------------- | --------------------------------------------------- |
| `http-headers`  | Retrieves HTTP response headers                     |
| `smb-protocols` | Identifies supported SMB protocol versions          |
| `ssh-hostkey`   | Retrieves SSH host key information and fingerprints |

### Observations

The earlier NSE scan already confirmed that:

* Apache was running on port 80.
* Tomcat was running on port 8180.
* Samba services were exposed through ports 139 and 445.
* SSH was running OpenSSH 4.7p1.
* SSH host key fingerprints were available for enumeration.

---

# 10. FTP Enumeration and HTTP Headers

## Steps 22–24

### Commands

```bash
nmap --script ftp-anon -p 21 192.168.56.102
```

```bash
curl -I http://192.168.56.102/
```

```bash
whatweb http://192.168.56.102
```

### Screenshot Evidence
<img width="1920" height="1003" alt="screenshot H lab 1" src="https://github.com/user-attachments/assets/15495c30-aedf-4727-bce5-f2cf7314691b" />


**Screenshot 8-1: Lab 1 – Anonymous FTP Testing, HTTP Header Retrieval and WhatWeb Fingerprinting**

### Results

The earlier Nmap NSE scan identified:

**FTP**

* FTP service: vsftpd 2.3.4
* Anonymous FTP login was allowed.

**HTTP**

* Apache HTTP Server 2.2.8
* Ubuntu-based server
* HTTP title: `Metasploitable2 - Linux`

The `curl -I` command was used to retrieve HTTP response headers without downloading the page body.

---

# 11. WhatWeb Web Fingerprinting

## Steps 25–27

### Commands

```bash
whatweb -v http://192.168.56.102
```

```bash
whatweb -a 1 http://192.168.56.102
```

```bash
whatweb -a 3 http://192.168.56.102
```

### Screenshot Evidence

<img width="1920" height="1003" alt="screenshot I lab 1" src="https://github.com/user-attachments/assets/7a8befe6-02e0-400a-adc7-d5cc1146b09a" />


**Screenshot 9-1: Lab 1 – WhatWeb Verbose and Aggression-Level Fingerprinting**

### Explanation

| **Command**    | **Purpose**                                      |
| -------------- | ------------------------------------------------ |
| `whatweb -v`   | Provides verbose WhatWeb output                  |
| `whatweb -a 1` | Performs low-aggression web fingerprinting       |
| `whatweb -a 3` | Performs more detailed/aggressive fingerprinting |

### WhatWeb Comparison

| **Level** | **Purpose**                           | **Expected Difference**                                     |
| --------- | ------------------------------------- | ----------------------------------------------------------- |
| Level 1   | Passive/low-aggression identification | Faster and less intrusive                                   |
| Level 3   | More detailed fingerprinting          | More probes and potentially more information                |
| Level 4   | Highest aggression                    | Most extensive fingerprinting and potentially more requests |

---

# 12. Advanced WhatWeb Fingerprinting

## Steps 28–30

### Commands

```bash
whatweb -a 4 http://192.168.56.102
```

```bash
whatweb --follow-redirect=always http://192.168.56.102
```

```bash
whatweb http://192.168.56.102 | tee ~/whatweb_results.txt
```

### Screenshot Evidence

<img width="1920" height="1003" alt="screenshot H lab 1" src="https://github.com/user-attachments/assets/8c83b362-ccc6-4fd1-8880-049fcf856bac" />


**Screenshot 10-1: Lab 1 – Advanced WhatWeb Fingerprinting, Redirect Following and Result Capture**

### Explanation

| **Command**                 | **Purpose**                                        |
| --------------------------- | -------------------------------------------------- |
| `whatweb -a 4`              | Performs the highest-aggression WhatWeb scan       |
| `--follow-redirect=always`  | Instructs WhatWeb to follow HTTP redirects         |
| `tee ~/whatweb_results.txt` | Displays the results and saves them to a text file |

---

# 13. Nmap Service Inventory

The full TCP service/version scan identified the following services on Metasploitable 2.

## TCP Service Inventory

| **Port** | **Protocol** | **State** | **Service** | **Version / Evidence**           |
| -------: | ------------ | --------- | ----------- | -------------------------------- |
|       21 | TCP          | Open      | FTP         | vsftpd 2.3.4                     |
|       22 | TCP          | Open      | SSH         | OpenSSH 4.7p1 Debian 8ubuntu1    |
|       23 | TCP          | Open      | Telnet      | Linux telnetd                    |
|       25 | TCP          | Open      | SMTP        | Postfix smtpd                    |
|       53 | TCP          | Open      | DNS         | ISC BIND 9.4.2                   |
|       80 | TCP          | Open      | HTTP        | Apache 2.2.8 Ubuntu              |
|      111 | TCP          | Open      | RPCBind     | RPCBind v2                       |
|      139 | TCP          | Open      | NetBIOS/SMB | Samba 3.X–4.X                    |
|      445 | TCP          | Open      | SMB         | Samba 3.0.20-Debian              |
|      512 | TCP          | Open      | rexec       | netkit-rsh rexecd                |
|      513 | TCP          | Open      | rlogin      | rlogind                          |
|      514 | TCP          | Open      | rsh         | Netkit rshd                      |
|     1099 | TCP          | Open      | Java RMI    | GNU Classpath grmiregistry       |
|     1524 | TCP          | Open      | Bindshell   | Metasploitable root shell        |
|     2049 | TCP          | Open      | NFS         | NFS v2–4                         |
|     2121 | TCP          | Open      | FTP         | ProFTPD 1.3.1                    |
|     3306 | TCP          | Open      | MySQL       | MySQL 5.0.51a-3ubuntu5           |
|     3632 | TCP          | Open      | distccd     | distccd v1 GNU 4.2.4             |
|     5432 | TCP          | Open      | PostgreSQL  | PostgreSQL 8.3.0–8.3.7           |
|     5900 | TCP          | Open      | VNC         | Protocol 3.3                     |
|     6000 | TCP          | Open      | X11         | Access denied                    |
|     6667 | TCP          | Open      | IRC         | UnrealIRCd                       |
|     6697 | TCP          | Open      | IRC/IRCS    | UnrealIRCd                       |
|     8009 | TCP          | Open      | AJP13       | Apache Jserv protocol v1.3       |
|     8180 | TCP          | Open      | HTTP        | Apache Tomcat/Coyote, Tomcat 5.5 |
|     8787 | TCP          | Open      | DRb         | Ruby DRb RMI                     |
|    41785 | TCP          | Open      | mountd      | RPC mountd v1–3                  |
|    43260 | TCP          | Open      | status      | RPC status v1                    |
|    57143 | TCP          | Open      | Java RMI    | GNU Classpath grmiregistry       |
|    60342 | TCP          | Open      | nlockmgr    | RPC lock manager v1–4            |

---

# 14. Important Reconnaissance Findings

The reconnaissance phase revealed a large attack surface on the intentionally vulnerable Metasploitable 2 system.

## Key Findings

### 1. Numerous Open TCP Ports

The full TCP scan identified **30 open TCP ports**.

This is significantly more than the number of services discovered through a basic default scan.

### 2. Anonymous FTP

The FTP service on port 21 allowed anonymous login.

This was confirmed through the NSE `ftp-anon` script.

### 3. Multiple Remote Access Services

The host exposed:

* Telnet
* rexec
* rlogin
* rsh
* SSH
* VNC

The presence of multiple remote-access services increases the number of services that would require security review.

### 4. SMB Services

Samba was exposed through ports 139 and 445.

NSE enumeration identified:

* NetBIOS name: `METASPLOITABLE`
* Workgroup information
* Samba version information
* SMB signing disabled

### 5. Web Services

The host exposed:

* Apache HTTP Server on port 80
* Apache Tomcat on port 8180
* AJP on port 8009

The HTTP service identified the page title:

`Metasploitable2 - Linux`

### 6. Database Services

The system exposed:

* MySQL on port 3306
* PostgreSQL on port 5432

### 7. RPC and NFS

RPC-related services were exposed through ports including:

* 111
* 2049
* 41785
* 43260
* 60342

### 8. Operating System

Nmap OS detection identified the target as a Linux system in the Linux 2.6.x kernel family.

---

# 15. Nmap vs WhatWeb

| **Feature**               | **Nmap**                           | **WhatWeb**                   |
| ------------------------- | ---------------------------------- | ----------------------------- |
| Primary Purpose           | Network and service reconnaissance | Web technology fingerprinting |
| Port Discovery            | Yes                                | No                            |
| Service Detection         | Yes                                | Limited to web services       |
| OS Detection              | Yes                                | No                            |
| HTTP Technology Detection | Yes                                | Yes                           |
| Web Framework Detection   | Limited                            | Stronger focus                |
| SMB Enumeration           | Yes                                | No                            |
| SSH Enumeration           | Yes                                | No                            |
| FTP Enumeration           | Yes                                | No                            |
| Web Fingerprinting        | Yes, through NSE                   | Primary purpose               |

Nmap provides a broad view of the host's network attack surface, while WhatWeb focuses specifically on identifying technologies used by web applications.

---

# 16. Student Questions and Answers

## Question 1 – What is reconnaissance?

Reconnaissance is the process of gathering information about a target system before performing deeper security testing. It can reveal IP addresses, ports, services, software versions and other technical information.

---

## Question 2 – What is the difference between host discovery and port scanning?

**Host discovery** determines whether a host is reachable or active.

**Port scanning** checks individual network ports to determine whether services are listening on them.

For example:

```bash
nmap -sn 192.168.56.102
```

performs host discovery, while:

```bash
nmap 192.168.56.102
```

performs a default port scan.

---

## Question 3 – What do open, closed and filtered mean?

| **State** | **Meaning**                                                                      |
| --------- | -------------------------------------------------------------------------------- |
| Open      | A service is actively listening on the port                                      |
| Closed    | The port is reachable but no service is listening                                |
| Filtered  | A firewall or filtering mechanism prevents Nmap from determining the exact state |

---

## Question 4 – What does `-sV` do?

The `-sV` option performs service/version detection. It sends additional probes to open ports to identify the service and, where possible, its version.

---

## Question 5 – What does `-O` do?

The `-O` option attempts to identify the target's operating system using TCP/IP fingerprinting and other observations.

In this lab, Nmap identified the target as a Linux system in the Linux 2.6.x family.

---

## Question 6 – What does `-A` do?

The `-A` option enables several advanced scanning features, including:

* OS detection
* Version detection
* Default NSE scripts
* Traceroute

It provides a more comprehensive picture of the target than a basic scan.

---

## Question 7 – What does `-p-` do?

The `-p-` option tells Nmap to scan all TCP ports from:

`1–65535`

This is useful because services can operate on ports outside the common/default port range.

---

## Question 8 – Why is UDP scanning slower than TCP scanning?

UDP is connectionless and many UDP services do not respond directly to probes. Nmap may therefore need to wait for responses or timeouts before deciding the state of a port.

In this lab, the full UDP scan took approximately 17 minutes, while the top-20 UDP scan completed much faster.

---

## Question 9 – What does `-sC` do?

The `-sC` option runs Nmap's default set of NSE scripts.

These scripts can gather additional information such as:

* FTP anonymous access
* SSH host keys
* HTTP information
* SMB information
* RPC details

---

## Question 10 – What HTTP information was discovered?

The HTTP service on port 80 was identified as:

* Apache 2.2.8
* Ubuntu
* DAV/2

The page title was:

`Metasploitable2 - Linux`

Tomcat was also identified on port 8180.

---

## Question 11 – What information was obtained from SMB, SSH and FTP?

### SMB

The scan identified:

* Samba
* NetBIOS name `METASPLOITABLE`
* Workgroup information
* SMB signing disabled

### SSH

SSH was identified as OpenSSH 4.7p1 and host key fingerprints were obtained.

### FTP

FTP was identified as vsftpd 2.3.4 and anonymous login was allowed.

---

## Question 12 – How does Nmap service detection differ from WhatWeb?

Nmap is primarily a network reconnaissance tool. It can discover ports, identify services, detect versions and perform OS detection.

WhatWeb is primarily a web application fingerprinting tool. It examines HTTP responses and identifies technologies, frameworks, servers and other web-related components.

---

## Question 13 – What is the difference between WhatWeb aggression levels 1, 3 and 4?

| **Level** | **Description**                                                   |
| --------- | ----------------------------------------------------------------- |
| 1         | Low-aggression fingerprinting with fewer requests                 |
| 3         | More detailed fingerprinting with additional probes               |
| 4         | Highest-aggression fingerprinting with the most extensive probing |

Higher aggression can provide more information but may generate more requests and have a greater impact on the target.

---

## Question 14 – Why must aggressive scanning and fingerprinting remain authorized?

Aggressive scans can generate a large number of requests and may affect system performance, trigger security controls or be interpreted as hostile activity.

Therefore, these techniques should only be performed against systems where explicit authorization has been provided.

In this assessment, scanning was restricted to the intentionally vulnerable Metasploitable 2 laboratory target.

---

# 17. Evidence Summary

| **Evidence**                    | **Completed** |
| ------------------------------- | ------------- |
| Target identification           | ✅             |
| Network connectivity test       | ✅             |
| Host discovery                  | ✅             |
| Default TCP scan                | ✅             |
| Service version detection       | ✅             |
| Intensive service detection     | ✅             |
| OS detection                    | ✅             |
| Aggressive Nmap scan            | ✅             |
| Full TCP port scan              | ✅             |
| Full TCP service/version scan   | ✅             |
| T4 timing scan                  | ✅             |
| Selected port scan              | ✅             |
| Ports 1–1024 scan               | ✅             |
| Full UDP scan                   | ✅             |
| Top 20 UDP scan                 | ✅             |
| Default NSE scripts             | ✅             |
| HTTP title enumeration          | ✅             |
| HTTP header enumeration         | ✅             |
| SMB protocol enumeration        | ✅             |
| SSH host key enumeration        | ✅             |
| FTP anonymous enumeration       | ✅             |
| HTTP header retrieval with curl | ✅             |
| WhatWeb fingerprinting          | ⬜             |
| WhatWeb aggression comparison   | ⬜             |
| WhatWeb redirect testing        | ⬜             |
| WhatWeb results saved to file   | ⬜             |

> Replace the remaining unchecked items after running Steps 24–30 and capturing the corresponding screenshots.

---

# 18. Final Reflection

This practical lab demonstrated how reconnaissance can provide a detailed understanding of a target system before vulnerability testing begins.

Using Nmap, I was able to identify the target host, discover open TCP and UDP ports, determine service versions, perform operating-system detection and use NSE scripts to collect additional information.

The full TCP scan was particularly useful because it revealed services running on ports that would not necessarily appear in a basic scan. The UDP scans also demonstrated the difference between TCP and UDP reconnaissance, especially the significantly longer scan time associated with UDP.

The NSE scripts provided additional information that was not available from a basic port scan. Examples included anonymous FTP access, SMB configuration, SSH host keys and HTTP information.

WhatWeb complemented Nmap by providing a more focused method of identifying technologies associated with the web service.

Overall, the lab demonstrated that reconnaissance is an important stage of cybersecurity assessment because it establishes the target's exposed attack surface and helps determine where further authorized testing should be focused.

---

# 19. Conclusion

The reconnaissance assessment successfully identified a large number of exposed services on the Metasploitable 2 target at `192.168.56.102`.

The most significant findings included:

* 30 open TCP ports
* Multiple UDP services
* Linux 2.6.x operating-system fingerprint
* Apache HTTP Server
* Apache Tomcat
* Samba
* MySQL
* PostgreSQL
* FTP
* SSH
* Telnet
* VNC
* NFS
* RPC services
* Anonymous FTP access
* SMB signing disabled

The exercise reinforced the importance of combining different reconnaissance techniques rather than relying on a single scan.

All testing was performed within the authorized laboratory environment against the intentionally vulnerable Metasploitable 2 machine.

---

# 20. Repository Evidence Structure

The GitHub repository should contain the README together with the evidence screenshots.

Recommended structure:

```text
LAB-1-Network-Service-Reconnaissance/
│
├── README.md
│
├── screenshots/
│   ├── lab1-step01-03.png
│   ├── lab1-step04-06.png
│   ├── lab1-step07-09.png
│   ├── lab1-step10-12.png
│   ├── lab1-step13-15.png
│   ├── lab1-step16-18.png
│   ├── lab1-step19-21.png
│   ├── lab1-step22-24.png
│   ├── lab1-step25-27.png
│   └── lab1-step28-30.png
│
└── results/
    └── whatweb_results.txt

---

## End of Lab 1 Evidence Report

**Student:** OMOWUMI SHARON
**Registration Number:** FDFC2617050
**Target:** Metasploitable 2 – `192.168.56.102`
