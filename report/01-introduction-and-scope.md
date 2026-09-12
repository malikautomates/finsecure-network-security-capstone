# Introduction and Scope

## Project Background

FinSecure Technologies Inc. is a financial services firm serving multinational corporations and financial institutions, with GlobalTech Industries as its flagship B2B client. Its infrastructure includes Active Directory servers, public-facing web servers, PostgreSQL database servers, Redis cache servers, and SFTP file-transfer servers.

At the start of this engagement, FinSecure was **not compliant** with SOX, PCI DSS, or GLBA. The immediate trigger was a confirmed breach of the web application server (detailed in [Incident Response](06-incident-response.md)), which exposed both the compliance gap and a set of concrete technical weaknesses in the network.

## Scope

1. Assess the existing network and identify the vulnerabilities that enabled the breach.
2. Redesign the network architecture to close those gaps and support ongoing compliance.
3. Procure and integrate the security technology needed to enforce the new design — NGFW, WAF, upgraded AAA/identity infrastructure, and SIEM.
4. Produce a comprehensive risk assessment and a governing Network Security Policy.
5. Design and justify a Zero Trust Architecture, with emphasis on securing remote employee connections and the B2B link to GlobalTech Industries.
6. Deliver staff training materials to support the transition to the new security controls.

## Objectives

- Bring FinSecure into compliance with SOX, PCI DSS, and GLBA.
- Implement Zero Trust principles — "never trust, always verify" — across users, devices, and network segments.
- Formalize a network security policy covering access control, monitoring, incident response, and data handling.

## Out of Scope

- Health-sector compliance frameworks (e.g., HIPAA) — FinSecure has no health-sector clients.
- Physical office relocation or facilities work beyond the data center controls referenced in the [Network Security Policy](../policy/network-security-policy.md).
