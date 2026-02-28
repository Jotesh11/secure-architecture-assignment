Task 4: Secure Architecture Design (Architectural Controls)

Goal:
This section proposes architectural security controls (not code fixes) to mitigate the high-risk threats identified in Task 3. Controls are grouped into required categories and mapped to threat reduction using defense-in-depth.

1) Identity and Access Management (IAM)
Controls:
  Central Auth Service issues short-lived session tokens (rotated/expired regularly).
  Multi-Factor Authentication (MFA) mandatory for Admin accounts.
  Role-Based Access Control (RBAC) for users/merchants/admins with “deny by default”.
  Just-in-time (JIT) privilege elevation for high-risk admin actions (refund approvals, payout changes).
  Separate identities for services (service accounts) with least privilege.

Why this control:
  Reduces T1 (credential stuffing) impact by MFA and tighter session handling.
  Reduces T5 (admin privilege escalation) by limiting privileges + JIT.
  Reduces account takeover blast radius (least privilege).

2) Network Segmentation
Controls:
  DMZ/Edge network contains only Web Frontends + API Gateway.
  Backend services run in a private network not reachable directly from the internet.
  Data layer isolation: databases and secrets store accessible only from required backend services.
  Separate Admin Plane:
    Admin Portal + Admin APIs isolated from customer/merchant flows (separate route / hostname / network policy).
    Admin access optionally restricted via VPN / bastion path.

Why this control:
  Limits lateral movement (reduces impact of T16 and any initial compromise).
  Prevents direct database exposure (reduces likelihood of T7).
  Admin separation reduces catastrophic “one bug = full takeover” failures.

3) Data Protection
Controls:
  TLS everywhere (client→gateway, gateway→services, services→databases).
  Encrypt data at rest for:
    User DB, Merchant DB, Transaction DB
    Audit log storage
  Tokenization of payment data:
    Store only gateway tokens (never raw card details).

  Integrity protections for ledger:
    Append-only transaction ledger patterns
    Backups + periodic integrity checks

Why this control:
  Prevents sniffing / MITM (T10, T11).
  Limits breach impact (T7) by encrypting sensitive data.
  Protects integrity of transaction records (T8) and reduces fraud.

4) Secrets Management
Controls:
  All secrets (API keys, DB creds, signing keys) stored in a central secrets store/vault.
  Rotation policy for secrets + short-lived credentials where possible.
  Strict access policies: services only read the secrets they require.
  No secrets in code or GitHub (config and CI secrets separation).

Why this control:
Directly mitigates T9 (secrets exposed) which is system-wide catastrophic.
Limits blast radius if one service is compromised.

5) Monitoring and Logging
Controls:
Centralized logging pipeline for API Gateway, Auth, Payment, Admin actions.
Immutable audit logs 
  Alerting rules for:
    Excess login failures (credential stuffing indicator)
    Admin privilege changes / payout modifications
    Refund spikes / unusual transaction patterns
  Correlation fields in logs:
    user/admin ID, IP/device metadata, request ID, timestamp, action result

Why this control
Prevents repudiation and supports incident response (T13).
Makes fraud harder to hide (T14).
Faster detection reduces impact even when prevention fails.

6) Secure Deployment Practices
Controls
CI/CD pipeline with:
signed artifacts / versioned deployments
dependency scanning
container image scanning
Environment separation with strict access control.
Infrastructure-as-code + config review 
Regular vulnerability scanning + patching cadence.

Why this control
Reduces introduction of insecure configurations and vulnerable dependencies.
Improves repeatability and reduces operational mistakes that cause breaches.

| Threat                   | Main Controls that mitigate it                                |
| ------------------------ | ------------------------------------------------------------- |
| T1 Credential stuffing   | MFA, rate limiting, login monitoring                          |
| T2 Session hijack        | TLS, short-lived tokens, secure session handling              |
| T4 Broken access control | RBAC, deny-by-default, admin/user separation                  |
| T6 Refund tampering      | Gateway validation + authorization boundaries + audit logging |
| T7 DB breach             | segmentation + encryption + monitoring                        |
| T8 Ledger tampering      | append-only design + audit logs + integrity checks            |
| T9 Secrets exposed       | secrets vault + rotation + no secrets in code                 |
| T12 API flooding         | WAF + throttling + rate limiting                              |
| T13 Missing logs         | centralized logs + audit requirements                         |
| T14 Log tampering        | immutable audit store                                         |
| T15 Admin phishing       | MFA + restricted admin access + alerts                        |
| T16 No admin separation  | admin/user plane separation + segmentation                    |
