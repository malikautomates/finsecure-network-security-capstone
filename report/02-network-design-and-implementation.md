# Network Design and Implementation

## Previous Architecture

The pre-engagement network (**Figure 1**) had almost no internal segmentation: a single WAF sat in front of the DMZ, and the DMZ itself hosted the public web servers, the web application servers, the SFTP servers, the Redis cache, *and* the PCI-DSS-relevant database side by side. A single flat internal VLAN network held Active Directory, the AAA server, and every department's endpoints together. This flat design is what allowed the October 3, 2024 breach (see [Incident Response](06-incident-response.md)) to escalate from a single vulnerable web endpoint into full lateral movement across the network.

![Previous network architecture](../diagrams/network-before.svg)
*Figure 1 — Previous network architecture: minimal segmentation, single WAF, no dedicated database isolation.*

## Redesigned Architecture

**Figure 2** shows the replacement design. It is built around defense-in-depth: each function-specific zone is isolated behind its own firewall boundary, so a compromise in one zone does not automatically grant access to the next.

![Redesigned network architecture](../diagrams/network-after.svg)
*Figure 2 — Redesigned network architecture: NGFW perimeter, dual active WAFs, three-tier application segmentation, and an isolated internal VLAN network.*

### Network Segments

**Customer Connection.** GlobalTech Industries and other B2B customers connect through a dedicated customer gateway and VPN connection over redundant ISP links, terminating at the NGFW rather than directly at any internal zone.

**Perimeter (NGFW + dual WAF).** A Next-Generation Firewall provides intrusion prevention, VPN termination, and data loss prevention at the network edge. Two Web Application Firewalls run in active-active mode in front of the application zone, giving both redundancy and inspection of all inbound application-layer traffic.

**DMZ.** Four public-facing web servers serve static content and handle the initial customer-facing request. Nothing in the DMZ can reach the database tier directly.

**Web Application Server Zone.** Two web application servers, sitting in a private intranet segment behind a load balancer and firewall, process business logic on behalf of the DMZ web servers. This isolation means a compromised public web server cannot reach application logic or data without crossing another firewall boundary.

**Database Zone.** Three PostgreSQL servers and two Redis cache servers sit in their own private, firewalled segment — a separate tier from both the DMZ and the web application zone, not "inside" either of them. The PostgreSQL instance holding cardholder and other regulated data is isolated behind an **additional**, dedicated firewall within this zone, so a breach of the general database zone still does not expose the PCI-DSS-relevant data. Two SFTP servers used for secure file transfer also live in this zone, now with key-based authentication enforced (see [Network Security Policy](../policy/network-security-policy.md)) rather than the default credentials exploited in the original breach.

**Internal VLAN Network.** Employee-facing infrastructure — two Active Directory servers, a secure DNS server, two SFTP servers for internal file transfer, and the AAA server — sits behind a multilayer switch, with HR, Finance, and IT endpoints each on their own VLAN. Segmenting by department limits lateral movement even if one internal VLAN is compromised.

**Monitoring.** A primary and backup SIEM ingest logs from the NGFW, WAFs, and internal infrastructure, giving redundant visibility and satisfying the continuous-monitoring requirements of SOX, PCI DSS, and GLBA.

## Compliance Alignment

- **PCI DSS** — Cardholder data is isolated in the dedicated Database Zone described above, segmented *behind* the DMZ and application tier (not within the DMZ), protected by an additional firewall, and covered by SIEM monitoring.
- **Data privacy (GDPR/CCPA-aligned practices)** — Personal data is segmented by zone, encrypted in transit via VPN, and access is restricted, audited, and controlled through role-based policies.
- **NIST Cybersecurity Framework** — The design maps to the Identify, Protect, Detect, Respond, and Recover functions through asset inventory, segmentation and access control, SIEM-based detection, the incident response process, and backup/disaster recovery planning.

Together, the NGFW, dual WAF, zone segmentation, and SIEM stack establish a secure, compliant baseline — the foundation the [Zero Trust Architecture](05-zero-trust-architecture.md) is then built on top of.
