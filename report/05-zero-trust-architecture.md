# Zero Trust Architecture

## Why Zero Trust, Specifically for FinSecure

None of SOX, PCI DSS, or GLBA mandate "Zero Trust" by name — but each one's actual requirements point directly at it:

| Regulation | Requirement | Zero Trust Principle It Maps To |
|---|---|---|
| **PCI DSS** | Strong access control, least privilege, MFA, network segmentation | Identity verification + micro-segmentation |
| **SOX** | Strong internal controls and protection of financial data from unauthorized access | Continuous identity verification, minimized trust boundaries |
| **GLBA** | Strong protection of nonpublic personal information (NPI) | Least-privilege access model |

Beyond compliance, three practical factors made Zero Trust the right call for FinSecure specifically:

- **Remote and B2B access is the norm, not the exception.** Employees connect remotely and GlobalTech Industries connects as an external partner — a perimeter-only model doesn't fit that reality.
- **Insider risk is a real line item.** As a financial institution handling high-profile client data, the cost of a single over-privileged internal account is disproportionately high.
- **Long-run cost.** The upfront cost of new hardware and specialized staff is real, but it is small next to the cost of another breach, incident response cycle, and compliance remediation like the one that triggered this engagement.

## Implementation Steps

![Zero Trust access decision flow](../diagrams/zero-trust-flow.svg)
*Figure 9 — Every access request — employee, remote VPN session, or the GlobalTech B2B connection — passes through the same four gates: identity verification, context-aware policy, NGFW enforcement, and continuous re-verification.*

The rollout followed the standard "never trust, always verify" sequence:

1. **Inventory users, devices, and data flow.** Catalogued every employee, contractor, application, and data repository, and mapped how data actually moves between them — surfacing the segmentation gaps described in the [Network Security Analysis](03-network-security-analysis.md).
2. **Define the protected surface.** Identified the Cardholder Data Environment and other critical internal resources (database and web application servers) as the highest-priority protected surface, and enforced micro-segmentation around them — the Database Zone and Web Application Zone described in the [network redesign](02-network-design-and-implementation.md).
3. **Implement strong Identity and Access Management.** Deployed a new AAA server integrated with Active Directory, delivering Single Sign-On (SSO), Multi-Factor Authentication (MFA), least-privilege access policies, and continuous authentication with behavioral analytics.
4. **Implement monitoring, logging, and automated response.** Added a dedicated SIEM instance for the Cardholder Data Environment alongside the existing SIEM, and integrated the AAA server with the NGFW so that a compromised device's access can be automatically revoked or quarantined without waiting on manual intervention.

## Benefits Realized

- **Reduced blast radius** — the "assume breach" posture, strong auth, and segmentation limit how far any single compromised credential or device can reach.
- **Better user experience despite tighter security** — SSO and context-aware access mean legitimate users authenticate less often, not more, while still tightening the actual control.
- **Faster, more automatic threat containment** — the AAA/NGFW integration quarantines a misbehaving device without a human in the loop for the first response.
- **Clear compliance evidence** — SSO, MFA, and behavioral logging give SOX/PCI/GLBA auditors a direct audit trail of who accessed what, when, and why.

## Challenges and How They Were Handled

| Challenge | How It Was Addressed |
|---|---|
| **Legacy system integration** — much of the existing IPS/IDS infrastructure predated Zero Trust design | Replaced the legacy devices with NGFWs as part of the same rollout rather than trying to retrofit Zero Trust onto them |
| **Cultural resistance to MFA** | Structured change management: training videos, documentation, and self-service tutorials ahead of enforcement |
| **24×7 operational complexity** | Coordinated the rollout across all departments — not just IT — to avoid disrupting live operations |
| **User friction on non-SSO-compliant applications** | Flagged as an ongoing remediation item; prioritized bringing remaining internal apps under the SSO umbrella (see [Recommendations](07-recommendations-and-conclusion.md)) |

## Cost Considerations

The upfront investment — new NGFW and AAA hardware, plus specialized implementation and ongoing operational staff — was significant. It is justified as a risk-transfer decision: the projected cost of another breach at the scale of the October 3, 2024 incident (client notification, regulatory exposure, reputational damage) is materially larger than the one-time and ongoing cost of the Zero Trust rollout.
