1. System Overview

This system is an Online Payment Processing Application that allows customers to pay merchants via a web application. The system integrates with an external Payment Gateway and a Core Banking System for settlement. It provides an Admin Portal for internal staff to manage users, merchants, disputes, refunds, and system configuration. The application is internet-facing and must defend against both external attackers and insider misuse.

2. Application Components (Required)
2.1 Frontend (Internet-facing)
    Customer Web Frontend: browsing, checkout, payment initiation
    Merchant Web Portal: view transactions, settlements, refunds (limited)
    Admin Portal: manage users/merchants, refunds, disputes, configuration (high privilege)

2.2 Backend Services
    API Gateway / Reverse Proxy (edge): single entry point, routing, throttling
    Auth Service: login, session/token issuance, MFA for admin
    Payment Service: payment initiation, status tracking, orchestration with gateway
    Merchant Service: merchant onboarding, merchant profile, payout preferences
    User Service: customer profile, payment methods (token references only)
    Transaction Service: transaction ledger, reconciliation records
    Notification Service: email/SMS receipts/alerts
    Admin Service: admin-only operations (refund approvals, risk rules, etc.)


2.3 Data Storage 
    User Database: customers, profiles, hashed credentials
    Merchant Database: merchants, KYC info, payout settings
    Transaction Database / Ledger: payments, refunds, chargebacks, settlement states
    Audit Log Storage: immutable-ish logs for investigations and compliance
    Secrets Store (logical component): API keys, DB creds, signing keys

2.4 External Dependencies (Required)
    Payment Gateway (external): processes card payments / redirects / 3DS
    Core Banking System (internal enterprise or partner): settlement, account debits/credits
    Email/SMS Provider: notifications
    Fraud/Risk Scoring Provider


3. Users and Roles

| Actor                          | Role                                        |
| ------------------------------ | ------------------------------------------- |
| Customer                       | Initiates payment, views history            |
| Merchant                       | Views transactions, settlement status       |
| Admin (Ops/Support)            | Refunds, disputes, merchant/user management |
| Finance/Admin (high privilege) | Settlement approvals, payout controls       |
| Payment Gateway                | External processor                          |
| Core Banking System            | Settlement + account movement               |
| External attacker              | Internet threat                             |
| Insider attacker               | Misuse by staff/merchant                    |


4. Data Types Handled
    Credentials: passwords (hashed), sessions/tokens, MFA secrets
    Personal data (PII): name, email, phone, address
    Merchant data: business details, payout account info, KYC docs
    Financial/transaction data: transaction IDs, amounts, status, refunds, chargebacks
    Payment data: should be tokenized; avoid storing raw card data
    Audit logs: admin actions, auth events, transaction changes


5. Trust Boundaries (this is key for marks)

A trust boundary exists where the trust level changes and extra controls are required.

TB1: Internet → Frontend
Users are untrusted; devices may be compromised.

TB2: Frontend → API Gateway
Traffic must be protected by TLS and strong auth; gateway enforces edge protections.

TB3: API Gateway → Backend Services (Private Network)
Services should not be directly reachable from the internet.

TB4: Backend Services → Databases
Highest-value zone; strict access controls, encryption, monitoring.

TB5: Backend → Payment Gateway
External dependency; requests must be authenticated, signed, and monitored.

TB6: Backend → Core Banking System
Critical integration; must be strongly authenticated and restricted.

TB7: Admin Plane vs User Plane
Admin portal + admin APIs must be isolated from normal customer/merchant paths.
