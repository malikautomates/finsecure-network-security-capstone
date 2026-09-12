# Risk Assessment

## Methodology

Risk was assessed using a standard threat–vulnerability–impact–likelihood model: for each critical asset, we identified plausible threats, the vulnerabilities that would let those threats materialize, the impact if they did, and how likely that is given current controls. Asset location and strategic importance were also weighted in, so that mitigation effort is directed at the risks that most threaten operational continuity and regulatory compliance — not just the highest raw severity score.

The full asset-by-asset breakdown is maintained separately as a living document: **[risk-assessment/risk-register.md](../risk-assessment/risk-register.md)**.

## Impact Scale

| Level | Definition |
|---|---|
| **Insignificant** | Minor, contained breach; resolved in days with minimal cost; no tangible harm. |
| **Minor** | Breach in one or two areas, resolved in under a week without senior management involvement; slight loss of efficiency, no tangible damage. |
| **Moderate** | Limited, possibly ongoing breach requiring management intervention, up to two weeks to resolve; some compliance cost and indirect reputational effect. |
| **Major** | Systemic breach lasting 4–8 weeks, requiring active senior leadership; customers and the public are likely informed. |
| **Catastrophic** | Breach lasting 3+ months with major customer loss, executive intervention, reputational damage, and possible disciplinary action. |
| **Doomsday** | Multiple severe breaches with indefinite impact — risk of bankruptcy/restructuring, legal action, and inability to meet organizational goals. |

## Likelihood Scale

| Level | Definition |
|---|---|
| **Rare** | Only in exceptional circumstances. |
| **Unlikely** | Could happen, but not expected under current controls. |
| **Possible** | Moderate likelihood; may be hard to control due to external factors. |
| **Likely** | Would not be surprising if it occurred. |
| **Almost Certain** | Expected to occur, likely sooner rather than later. |

## Highest-Priority Risks (Extreme)

The five highest-rated risks in the register, all rated **Extreme**:

| Asset | Threat | Top Control Recommendation |
|---|---|---|
| Customer/financial data | Data breach via SQL injection | Encryption at rest & in transit, strict RBAC, database activity monitoring, admin MFA |
| Security event data (SIEM) | Log tampering, delayed detection | Full log coverage, real-time alerting, IDS/IPS integration, regular tuning |
| User credentials / AD | Privilege escalation, account hijacking | Enforce MFA, least-privilege review, login-attempt auditing |
| Authentication (AAA) | Credential theft, denial of service | Strong password policy, MFA, RADIUS in the backbone, failed-access monitoring |
| Banking service availability | Partial/total service loss | Formal incident response, business continuity and disaster recovery plans, communication matrix with GlobalTech |

Full details — including the High- and Medium-rated risks around firewall configuration, web application attacks, cache/session data, and physical infrastructure — are in the [risk register](../risk-assessment/risk-register.md).

## Relationship to Other Controls

This risk assessment is not a standalone artifact — every "Extreme" and "High" risk maps directly to a control already implemented in the [network redesign](02-network-design-and-implementation.md) or codified in the [Network Security Policy](../policy/network-security-policy.md). Where a gap remained un-mitigated by the existing architecture (for example, the lack of a RADIUS device in the backbone), it is called out explicitly as a follow-up action.
