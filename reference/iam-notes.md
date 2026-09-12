# Reference Notes — Identity & Access Management (IAM) Module

> **Supplementary material.** This is a lightly cleaned summary of the group's IAM module working notes, not a rewritten standalone report like the [flagship report](../report/full-report.md). It's included for completeness and context.

## Objective

Implement a secure IAM solution on Microsoft Azure covering both FinSecure employees and GlobalTech Industries personnel, enforcing least privilege and satisfying SOX/PCI-DSS/GLBA access-control requirements.

## Key Work Completed

- **User and group management** — individual IAM accounts for FinSecure and GlobalTech users, organized into role-based groups rather than shared credentials.
- **Policy design** — identity-based policies (permissions tied to a user/group) and resource-based policies (permissions tied to specific Azure resources, e.g., Azure AD, Blob Storage) layered for fine-grained, auditable access.
- **Multi-Factor Authentication** — enforced for all IAM users via Azure MFA (SMS, phone call, or authenticator app).
- **Password policy** — enforced complexity, minimum length, and regular rotation.
- **Role-Based Access Control (RBAC)** — access delegated by job role rather than by individual, improving both security and accountability.
- **Monitoring and logging** — Azure Activity Logs integrated with Azure Security Center, with alerting configured for suspicious IAM activity.
- **Documentation and training** — IAM policies, roles, groups, and MFA configuration documented; training delivered to both FinSecure and GlobalTech personnel on MFA usage and incident-reporting procedures.

## Relationship to the Flagship Report

This module is the Azure-native precursor to the on-prem [Zero Trust Architecture](../report/05-zero-trust-architecture.md) in the flagship report: the same RBAC, MFA, and least-privilege principles applied here to Azure IAM are what the flagship report later generalizes into a full Zero Trust rollout across FinSecure's on-prem AAA server and Active Directory.
