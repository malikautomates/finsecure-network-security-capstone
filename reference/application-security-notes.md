# Reference Notes — Application Security Module

> **Supplementary material.** This is a lightly cleaned summary of the group's Application Security module working notes, not a rewritten standalone report like the [flagship report](../report/full-report.md). It's included for completeness and context.

## Objective

Secure the web application FinSecure Technologies Inc. built for its clients — covering authentication, financial data handling, and compliance reporting for GlobalTech Industries — against the application-layer threats identified in the [Network Security Analysis](../report/03-network-security-analysis.md) (notably SQL injection and XSS).

## Key Application Features Assessed

- **Authentication and authorization** — secure login with strong password policy and MFA; RBAC restricting access by job responsibility.
- **Financial dashboard and reporting** — real-time transaction views and compliance-status reporting, with automated compliance checks for SOX.
- **Document management** — centralized, version-controlled storage for financial documents with full audit trails.
- **Client communication** — a secure messaging and document-sharing channel between FinSecure advisors and clients.
- **Digital signing** — e-signature functionality with logged approvals for auditability.
- **Audit trail and logging** — comprehensive activity logging across user actions, data changes, and system modifications, supporting forensic analysis if an incident occurs.
- **Data encryption** — end-to-end encryption for financial data at rest and TLS in transit.

## Relationship to the Flagship Report

The vulnerabilities actually confirmed against this application — SQL injection, XSS, and weak SFTP authentication — are documented in full, with methodology and remediation, in [Network Security Analysis](../report/03-network-security-analysis.md). The WAF, TLS enforcement, and MFA/RBAC controls recommended there are the direct fix for the gaps this module's design intended to prevent in the first place.
