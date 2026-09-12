# Presentation Walkthrough

A step-by-step, readable version of [`FinSecure-Capstone-Presentation.pptx`](FinSecure-Capstone-Presentation.pptx) — the same 17 slides, in order, with their diagrams/screenshots and a short explanation of what each one is doing. Use this if you want to skim the deck's content without opening PowerPoint.

---

## Step 1 — Title

Opens the deck: *Fortifying B2B Network Security for Regulatory Compliance*, a FinSecure Technologies Inc. case study by Group 3 (Case Studies, Issues & Capstone Project in Network Security, University of Winnipeg, Fall 2024).

## Step 2 — Agenda

Lays out the eight-part arc the rest of the deck follows: client background → the breach → methodology → network redesign → Zero Trust → risk & policy → incident response → results.

## Step 3 — Client Background

Introduces FinSecure Technologies Inc., its flagship B2B client GlobalTech Industries, and the three regulations it must satisfy at once — SOX, PCI DSS, and GLBA — while explicitly noting HIPAA/health-sector rules never applied.

## Step 4 — The Problem: A Confirmed Breach

States the trigger for the entire engagement: an October 3, 2024 breach of the web application server via SQL injection and weak default SFTP credentials, discovered while FinSecure was still non-compliant with all three regulations.

## Step 5 — Objectives & Scope

Frames the three project objectives — achieve compliance, implement Zero Trust, formalize governance — and draws an explicit scope boundary so the engagement doesn't creep into unrelated work like health-sector compliance.

## Step 6 — Methodology: Three Complementary Approaches

Explains why three testing methods were used together rather than one: automated scanning (Nmap + OWASP ZAP) for broad coverage, manual penetration testing (Metasploit) to confirm real exploitability, and a policy/configuration audit to catch process gaps the tools can't see.

## Step 7 — Live Evidence: Scanning FinSWebApp

![Nmap scan of the production FinSWebApp instance](../evidence/pentest/nmap-scan-production.jpg)

![OWASP ZAP vulnerability scan of FinSWebApp](../evidence/pentest/zap-vulnerability-scan.jpg)

These are real scans, not mockups — Nmap (left) and OWASP ZAP (right) run from the group's own Kali Linux workstation against the group's own deployed `FinSWebApp` instance on Azure App Service, confirming a small external attack surface but flagging missing security headers and a vulnerable JavaScript library.

## Step 8 — The Attack Path, Reconstructed

![Reconstructed attack path](../diagrams/attack-path.svg)

Reconstructs exactly how the October 3rd attacker moved through the network — SQL injection entry point, credential harvesting, lateral movement into SFTP via default logins, and finally data exfiltration.

## Step 9 — Before: A Flat, Under-Segmented Network

![Previous network architecture](../diagrams/network-before.svg)

Shows the pre-engagement network: a single WAF, no internal segmentation, and the cardholder database sitting in the same zone as the public web servers — the exact design flaw that let one compromised endpoint reach the database directly.

## Step 10 — After: Defense-in-Depth Segmentation

![Redesigned network architecture](../diagrams/network-after.svg)

Shows the rebuilt architecture: an NGFW plus dual active WAFs at the perimeter, three-tier isolation (DMZ → App Zone → Database Zone), a dedicated extra firewall around cardholder data, and per-department VLANs to contain any future breach.

## Step 11 — Why Zero Trust, Specifically for FinSecure

Maps each regulation to the Zero Trust principle it implicitly demands — PCI DSS to micro-segmentation, SOX to continuous verification, GLBA to least-privilege access — framing Zero Trust as a consequence of taking compliance seriously, not a trend FinSecure chased.

## Step 12 — How It Works: Never Trust, Always Verify

![Zero Trust access decision flow](../diagrams/zero-trust-flow.svg)

Walks through the four-stage access-decision flow — identity verification, context-aware policy check, NGFW enforcement, and continuous re-verification — that now governs every request, whether from an employee, a remote VPN session, or the GlobalTech B2B connection.

## Step 13 — Highest-Priority Risks (Rated Extreme)

Surfaces the five highest-rated risks from the full 18-item risk register, each one mapped directly to a control already shown in the redesign or the Zero Trust rollout — the register isn't a separate compliance exercise, it's what justified the architecture.

## Step 14 — What Now Governs the Network

Summarizes the five key sections of the updated Network Security Policy, including the two sections — Remote Access & Removable Media, and Third-Party/Vendor Risk — that were added during the rebuild to close a real gap in the original document.

## Step 15 — How We Responded to the Breach

Walks through the five-step incident response as a timeline, not a checklist: contain, investigate, notify, recover, review — with notification running in parallel with recovery rather than after it, since GLBA and client trust both demand speed.

## Step 16 — Compliance Achieved — What's Next

Closes the loop: confirmed compliance status against SOX, PCI DSS, GLBA, and the NIST Cybersecurity Framework on one side, and five concrete follow-up recommendations (recurring audits, ongoing training, IR drills) on the other — compliance is a status achieved, not a permanent state.

## Step 17 — Thank You / Credits

Closing slide crediting Group 3, the course, and the University of Winnipeg, with a specific callout of individual contribution to the Network Security Analysis section and this rebuild.
