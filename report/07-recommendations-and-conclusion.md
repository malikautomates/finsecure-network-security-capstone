# Recommendations and Conclusion

## Project Recap

This engagement started from a confirmed incident — a SQL injection breach of FinSecure's web application server — and a compliance gap across SOX, PCI DSS, and GLBA. From there, the project:

1. Assessed the existing (flat, weakly segmented) network and reconstructed exactly how the breach happened.
2. Redesigned the network around defense-in-depth zone segmentation, an NGFW, and dual active WAFs.
3. Isolated the Cardholder Data Environment behind its own dedicated firewall.
4. Rolled out a Zero Trust Architecture — new AAA/IAM infrastructure delivering SSO, MFA, RBAC, and context-aware access, automatically integrated with the NGFW for threat containment.
5. Added a dedicated SIEM for the Cardholder Data Environment on top of the existing SIEM, for continuous monitoring.
6. Formalized all of the above into a governing [Network Security Policy](../policy/network-security-policy.md) and [risk register](../risk-assessment/risk-register.md).

Despite real friction — legacy-system integration, cultural resistance to MFA, and the operational complexity of a 24×7 environment — the project delivered a network that is materially more resilient and brings FinSecure into alignment with SOX, PCI DSS, and GLBA.

## Future Recommendations

- **Regular security audits.** Combine in-house reviews with third-party audits on a recurring schedule, not only after an incident.
- **Ongoing training and awareness.** Keep cybersecurity training current for all staff, with role-specific tracks for IT/SOC.
- **Scalability planning.** Every new device or service added to the network must be integrated into the Zero Trust model from day one — Zero Trust degrades quickly if new assets are added outside the framework.
- **Enhanced incident response planning.** Run regular IR drills and feed the lessons from each one back into the plan, rather than only updating it after a real incident.
- **Close the remaining SSO gap.** Bring the non-SSO-compliant internal applications flagged in the [Zero Trust rollout](05-zero-trust-architecture.md) fully into the SSO/MFA umbrella to remove the last source of user friction and shadow risk.
