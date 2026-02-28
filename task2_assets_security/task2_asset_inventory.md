Task 2:Asset Identification and Security Objectives

1. Asset Identification
In an online payment processing system, assets include any data, service, or component whose compromise would impact the system’s confidentiality, integrity, availability, or accountability.

Below is the identified asset inventory:

| Asset ID | Asset Name                              | Description                                          | Category             | Sensitivity Level |
| -------- | --------------------------------------- | ---------------------------------------------------- | -------------------- | ----------------- |
| A1       | User Credentials                        | Passwords (hashed), sessions, MFA tokens             | Authentication       | Critical          |
| A2       | Customer Personal Data                  | Name, email, address, phone                          | Personal Data        | High              |
| A3       | Merchant Personal & KYC Data            | Business registration, payout accounts               | Personal/Financial   | Critical          |
| A4       | Transaction Records                     | Payment ID, amount, timestamps, status               | Financial            | Critical          |
| A5       | Payment Tokens                          | Tokenized card references                            | Financial            | Critical          |
| A6       | Admin Accounts                          | Privileged system accounts                           | Authentication       | Critical          |
| A7       | Business Logic                          | Payment validation, refund rules, settlement logic   | Application Logic    | Critical          |
| A8       | Audit Logs                              | Login logs, admin actions, transaction modifications | Monitoring           | High              |
| A9       | API Keys & Secrets                      | Gateway credentials, DB credentials, signing keys    | Secrets              | Critical          |
| A10      | Databases (User, Merchant, Transaction) | Structured stored data                               | Infrastructure       | Critical          |
| A11      | Core Banking Integration                | Settlement processing interface                      | External Integration | Critical          |
| A12      | Payment Gateway Integration             | Card processing interaction                          | External Integration | Critical          |


3. Mapping Assets to Security Objectives

Security objectives include:
Confidentiality (C): prevent unauthorized disclosure
Integrity (I): prevent unauthorized modification
Availability (A): ensure system uptime and accessibility
Accountability (Ac): ability to trace actions to identities

| Asset ID | Confidentiality | Integrity | Availability | Accountability | Why                                            |
| -------- | --------------- | --------- | ------------ | -------------- | ---------------------------------------------- |
| A1       | ✓               | ✓         |              | ✓              | Credential compromise enables account takeover |
| A2       | ✓               | ✓         |              | ✓              | PII exposure leads to privacy breach           |
| A3       | ✓               | ✓         |              | ✓              | Merchant fraud risk                            |
| A4       | ✓               | ✓         | ✓            | ✓              | Financial ledger must be correct and auditable |
| A5       | ✓               | ✓         |              |                | Payment data must never leak                   |
| A6       | ✓               | ✓         |              | ✓              | Admin misuse must be traceable                 |
| A7       |                 | ✓         | ✓            |                | Tampering with logic enables fraud             |
| A8       | ✓               | ✓         | ✓            | ✓              | Logs support forensic investigation            |
| A9       | ✓               | ✓         |              |                | Secret leakage = full system compromise        |
| A10      | ✓               | ✓         | ✓            |                | DB compromise breaks system                    |
| A11      | ✓               | ✓         | ✓            |                | Settlement must be secure and reliable         |
| A12      | ✓               | ✓         | ✓            |                | Payment processing must remain correct         |

4. Security Objective Analysis

4.1 Confidentiality

Critical for:
  Credentials
  Payment tokens
  Personal data
  Merchant payout details
  Secrets

Failure leads to:
  Financial theft
  Identity theft
  Regulatory fines
  Reputation damage

  4.2 Integrity

Critical for:
  Transaction records
  Refund processing
  Settlement logic
  Admin actions
  Business rules

If integrity fails:
  Funds can be redirected
  Fake refunds issued
  Financial reconciliation breaks

4.3 Availability

Critical for:
  Payment service
  API gateway
  Transaction database
  Banking integration

If unavailable:
  Merchants lose revenue
  Customers cannot pay
  Financial damage occurs immediately

4.4 Accountability

Critical for:
  Admin operations
  Refund approvals
  Transaction modifications
  Login attempts

Without accountability:
  Fraud cannot be investigated
  Insider misuse goes undetected
  Regulatory non-compliance

  
