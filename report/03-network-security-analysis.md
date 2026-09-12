# Network Security Analysis

## Methodology

The investigation into the unauthorized access incident combined three complementary approaches so that findings from one method could corroborate another:

1. **Automated network scanning** — broad, repeatable coverage of open ports, exposed services, and known-vulnerable software versions across every server and network device.
2. **Manual penetration testing** — targeted exploitation attempts against the specific weaknesses the automated scans flagged, to confirm they were actually exploitable rather than theoretical.
3. **Security audits** — a policy- and configuration-level review of access controls, encryption, and network segmentation against SOX, PCI DSS, and GLBA requirements.

## Tools and What Each One Found

| Tool | Role | Key finding |
|---|---|---|
| **Nmap** | Port/service discovery, asset mapping | Web servers exposed port 80 (HTTP) with no enforced HTTPS redirect; SSH (port 22) reachable on internal servers, a brute-force risk if credentials are weak. |
| **OWASP ZAP** | Automated vulnerability scanning | Missing security headers (Content-Security-Policy, anti-clickjacking, Strict-Transport-Security), a vulnerable JavaScript library, and cookies issued without the `Secure` flag. |
| **Metasploit** | Exploit verification | Confirmed that the SQL injection flaw in the internally built web application was practically exploitable, not just theoretical — payloads returned real backend data. |
| **Wireshark** | Traffic analysis | High-volume, repeated HTTP connections from the web server to a single external IP — consistent with data exfiltration rather than normal traffic patterns. |
| **Firewall/WAF log review (via SIEM)** | Correlation | A specific web endpoint showed a sustained pattern of SQL injection attempts, corroborating the Metasploit findings and pinpointing the entry point later confirmed in the incident timeline. |
| **Policy & configuration audit** | Compliance review | Several critical servers were not properly segmented, allowing lateral movement between network segments — the same gap closed in the [redesigned architecture](02-network-design-and-implementation.md). |

## Live Reconnaissance and Scanning Evidence

The scans below were run directly against FinSecure's own test deployment (`FinSWebApp`, hosted on Azure App Service) and its pre-production staging server, using the tools listed above from a Kali Linux workstation.

![FinSWebApp login page](../evidence/pentest/finswebapp-login.jpg)
*Figure 3 — The actual target of this assessment: the FinSWebApp login page, the internally developed web application at the center of the incident.*

![Nmap scan of the production FinSWebApp instance](../evidence/pentest/nmap-scan-production.jpg)
*Figure 4 — Nmap service scan against the live, Azure-hosted FinSWebApp instance: only ports 80 and 443 are exposed externally, with a valid Azure-issued TLS certificate.*

![Confirming the FinSWebApp production hostname and IP](../evidence/pentest/uncover-ip-address.jpg)
*Figure 5 — Resolving the FinSWebApp production hostname to its Azure App Service IP address as part of reconnaissance.*

![OWASP ZAP vulnerability scan of FinSWebApp](../evidence/pentest/zap-vulnerability-scan.jpg)
*Figure 6 — OWASP ZAP automated scan results for FinSWebApp: 12 alerts, including a missing Content-Security-Policy header and a vulnerable JavaScript library — the class of gap closed by the WAF and hardened headers in the [network redesign](02-network-design-and-implementation.md).*

![Nmap scan of the pre-production staging server](../evidence/pentest/nmap-scan-staging.jpg)
*Figure 7 — Nmap scan of the pre-production staging server: SSH (22), HTTP (80), and HTTPS (443) all open, with the HTTPS service presenting a certificate that expired in 2010 — exactly the kind of stale, unmanaged TLS configuration the redesign's certificate and patch-management policy is meant to catch before a server reaches production.*

## Vulnerabilities Discovered

- **SQL Injection** in an internally developed web application, allowing unauthorized access to backend data.
- **Cross-Site Scripting (XSS)** in the same web application, which could allow session hijacking or arbitrary script execution against other users.
- **Weak authentication on SFTP servers** — default credentials (e.g., `admin`/`admin`) left them exposed to brute-force access.
- **Missing security headers and an outdated client-side library**, confirmed by the OWASP ZAP scan above — lower-severity findings, but consistent with the same "hardening was skipped under deadline pressure" pattern that produced the SQL injection flaw.

## Attack Path

The path an attacker actually followed, reconstructed from the SIEM, firewall logs, and traffic analysis above:

![Attack path](../diagrams/attack-path.svg)
*Figure 8 — Reconstructed attack path: SQL injection entry point → credential harvesting → lateral movement to SFTP → data exfiltration.*

1. **Entry point** — SQL injection against the internally developed web application, over HTTP on port 80.
2. **Credential harvesting** — the same injection flaw exposed enough backend information to recover working credentials.
3. **Lateral movement** — those credentials, combined with SFTP servers still using default logins, let the attacker reach and browse file shares beyond the original web application.
4. **Exfiltration** — high-volume, repeated HTTP connections to a single external IP indicated sensitive files being moved off the network.

## Assessment of Current Security Posture (Pre-Remediation)

At the time of the incident, FinSecure's security posture was **moderate at best**, with clear, specific gaps: authentication security, vulnerability management, and internal segmentation. These gaps are addressed directly by the [network redesign](02-network-design-and-implementation.md), the [Zero Trust Architecture](05-zero-trust-architecture.md), and the hardening requirements in the [Network Security Policy](../policy/network-security-policy.md).

## Recommended Security Solutions

- **Perimeter**: upgrade to an NGFW with integrated VPN, DLP, and IPS to filter and monitor traffic before it reaches internal zones.
- **Application layer**: deploy a WAF to block SQL injection and XSS at the edge, and enforce current TLS certificates on all client-facing communication.
- **Internal segmentation**: implement VLANs per department (HR, Finance, IT) to contain lateral movement.
- **Authentication**: enforce MFA for all users — especially privileged access — require strong, regularly rotated passwords, and eliminate default credentials outright.
- **Training**: run regular security-awareness training focused on phishing prevention, credential hygiene, and incident reporting.
- **Vulnerability management**: schedule recurring OWASP ZAP and Nmap scans and enforce the patch-management SLAs defined in the [Network Security Policy](../policy/network-security-policy.md).
