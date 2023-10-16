
## links naar tools
[https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS "https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS")

https://gtfobins.github.io/

Image spull:
https://www.aperisolve.com/
## Veel gebruikte commando's
**Extract tar.gz bestand**
```bash
tar xzf snort3-community-rules.tar.gz -C /usr/local/etc/rules/
```

Nmap
bij windows 1. -Pn 
-p- toevogen als je niet veel vind. Dit zoekt voor elke poort, ook hogere
```bash
nmap -A -T4 <ip> -oN <bestandnaam>
```

```bash
nmap -sT <ip> -p 1-1000
```

**Hydra**
```bash
commando: ssh attack

# hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.1.105 -t 4 ssh
```

1. **Nmap** (Network Mapper):
    
    - Nmap is een krachtige open-source netwerkscanner die wordt gebruikt voor het ontdekken en in kaart brengen van netwerkapparaten en hun open poorten. Het kan informatie verschaffen over hosts, services en hun configuraties.
2. **Gobuster**:
    
    - Gobuster is een hulpprogramma voor directory- en bestandsbrute-forcing. Het wordt vaak gebruikt om verborgen bestanden en directories op een webserver te vinden door verschillende bestands- en directorynamen uit te proberen.
3. **Nikto**:
    
    - Nikto is een open-source webserver-scanner die bekendstaat om het identificeren van kwetsbaarheden in webtoepassingen en webservers. Het scant een doelsite op potentiële beveiligingsproblemen, zoals verouderde software en misconfiguraties.
4. **FFuF** (Fuzz Faster U Fool):
    
    - FFuF is een hulpmiddel voor het uitvoeren van fuzzing-aanvallen op webtoepassingen en andere doelsystemen. Het kan worden gebruikt om verschillende parameters en payloads te testen om kwetsbaarheden, zoals SQL-injecties of cross-site scripting (XSS), op te sporen.
5. **Wpscan**:
    
    - Wpscan is een specifieke tool voor het scannen van WordPress-websites. Het kan worden gebruikt om kwetsbaarheden in WordPress-thema's, plugins en configuraties te detecteren. Ook kan het informatie verzamelen over de WordPress-versie en actieve gebruikers.
## Tools voorbeleden
**1. Netwerkbeveiliging:**

- Firewall-tools:
    - Voor Windows: Windows Firewall, Sophos XG Firewall.
    - Voor Linux: iptables, UFW (Uncomplicated Firewall).
- IDS/IPS-tools:
    - Snort, Suricata, Bro/Zeek.
- Netwerkanalysesoftware:
    - Wireshark, tcpdump.
- Draadloze netwerkbeveiliging:
    - Aircrack-ng, Kismet.

**2. Besturingssysteembeveiliging:**

- Beveiligingsconfiguratietools:
    - Microsoft Baseline Security Analyzer (MBSA), Lynis (Linux).
- Patchmanagementtools:
    - WSUS (Windows Server Update Services), YUM (Linux).
- Toegangsbeheer- en audittools:
    - SELinux (Linux), Windows Security and Event Logs.

**3. Malware-analyse:**

- Antivirus- en antimalware-tools:
    - Windows Defender, ClamAV (Linux).
- Sandboxing-tools:
    - Cuckoo Sandbox, Joe Sandbox.
- Reverse-engineering-tools:
    - IDA Pro, Ghidra.

**4. Cryptografie:**

- Cryptografische libraries en tools:
    - OpenSSL, GnuPG (GPG).
- SSL/TLS-analysetools:
    - OpenSSL, Wireshark.

**5. Webbeveiliging:**

- Web Application Scanners:
    - OWASP ZAP, Burp Suite.
- Beveiligingsheaders en HTTPS-tools:
    - SSL Labs, OWASP Secure Headers Project.
- WAF-tools:
    - ModSecurity, AWS WAF.

**6. Sociale techniek en phishing:**

- Phishing-simulatietools:
    - GoPhish, SET (Social-Engineer Toolkit).

**7. Beveiligingsincidenten en respons:**

- SIEM-tools (Security Information and Event Management):
    - Splunk, ELK Stack (Elasticsearch, Logstash, Kibana).
- Forensische tools:
    - Autopsy, The Sleuth Kit.

**8. Cloudbeveiliging:**

- Cloudbeveiligingstools van providers:
    - AWS Identity and Access Management (IAM), Azure Active Directory.
- Cloudbeveiligingstools van derden:
    - Palo Alto Networks Prisma Cloud, Trend Micro Cloud One.

**9. IoT-beveiliging:**

- IoT-beveiligingshulpmiddelen:
    - Shodan, IoT Inspector.

**10. Red teaming en penetratietesten:** - Penetratietestframeworks: - Metasploit, OWASP Amass. - Vulnerability scanners: - Nessus, OpenVAS.

**11. Compliance en regelgeving:** - Compliance auditing tools: - Qualys, Tenable.io.

**12. Cyber Threat Intelligence (CTI):** - Threat Intelligence platforms: - Anomali ThreatStream, MISP (Malware Information Sharing Platform & Threat Sharing).

**13. Beveiliging van mobiele apparaten:** - Mobile Device Management (MDM) tools: - MobileIron, AirWatch (VMware Workspace ONE).