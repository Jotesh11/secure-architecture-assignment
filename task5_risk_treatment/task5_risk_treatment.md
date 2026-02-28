Task 5: Risk Treatment and Residual Risk
1. Risk Treatment Strategy
The organization evaluates high-risk threats identified in Task 3 and applies one of the following strategies:
Mitigate: Reduce likelihood or impact via controls
Transfer: Shift financial impact (e.g., insurance, contractual agreements)
Avoid: Eliminate risky feature or behavior
Accept: Acknowledge and monitor low or unavoidable risk

2. Risk Treatment Table
| Threat ID | Threat Summary             | Risk Level | Treatment Strategy  | Justification                                                            |
| --------- | -------------------------- | ---------- | ------------------- | ------------------------------------------------------------------------ |
| T1        | Credential stuffing        | High       | Mitigate            | MFA, rate limiting, login monitoring reduce likelihood                   |
| T2        | Session hijacking          | High       | Mitigate            | TLS, short-lived tokens, secure cookie settings                          |
| T4        | Broken access control      | High       | Mitigate            | RBAC + deny-by-default reduces privilege abuse                           |
| T5        | Admin privilege escalation | High       | Mitigate            | JIT access + MFA + audit logging                                         |
| T6        | Refund/payment tampering   | High       | Mitigate            | Strong validation + authorization + ledger integrity                     |
| T7        | Database breach            | High       | Mitigate + Transfer | Encryption + segmentation; cyber insurance for residual financial impact |
| T8        | Ledger tampering           | High       | Mitigate            | Append-only design + integrity monitoring                                |
| T9        | Secrets exposure           | High       | Mitigate            | Central secrets vault + rotation                                         |
| T10       | MITM attack                | High       | Avoid + Mitigate    | Enforce TLS only; block HTTP entirely                                    |
| T12       | API DoS                    | High       | Mitigate            | WAF + rate limiting + scaling                                            |
| T13       | Missing logs               | High       | Mitigate            | Mandatory audit logging                                                  |
| T14       | Log tampering              | High       | Mitigate            | Immutable log storage                                                    |
| T15       | Admin phishing             | High       | Mitigate            | MFA + admin network restriction                                          |
| T16       | No admin separation        | High       | Avoid               | Architectural redesign separating admin plane                            |


3. Residual Risk Explanation

Even after implementing strong architectural controls, some risk remains.

3.1 Residual Authentication Risk
Even with MFA, phishing-resistant mechanisms, and monitoring, sophisticated attackers may still compromise user accounts via:
  Social engineering
  Zero-day browser exploits
  Device compromise
Residual risk remains Medium due to human factors.

3.2 Residual Data Breach Risk

Encryption protects data at rest, but:
  Insider misuse is still possible
  Compromised admin credentials may allow legitimate decryption access
Residual risk remains Medium.

3.3 Residual DoS Risk

Rate limiting and WAF reduce DoS likelihood, but:
  Large-scale distributed attacks may still overwhelm infrastructure
  Upstream network providers may be saturated
Residual risk remains Medium.

3.4 Residual Insider Threat Risk

Logging and monitoring detect misuse but cannot completely prevent:
  Malicious administrators
  Collusion between insiders
Residual risk remains Low–Medium, depending on governance controls.

4. Risk Acceptance Statement

The organization acknowledges that:
  Zero risk is impossible in an internet-facing financial system.
  Risk must be continuously assessed and monitored.
  Residual risks are documented and approved by management.
Risk acceptance decisions are reviewed periodically as part of governance and compliance processes.

5. Risk Treatment Summary
Most high-risk threats were mitigated through architectural controls.
Certain risks were transferred via insurance and external payment processor agreements.
Some architectural weaknesses were avoided through redesign (admin separation).
Remaining risks are monitored through logging and incident response procedures.
