Task 3: STRIDE Threat Modeling
1. Threat Modeling Approach

We use the STRIDE methodology:
S – Spoofing
T – Tampering
R – Repudiation
I – Information Disclosure
D – Denial of Service
E – Elevation of Privilege

Threats are analyzed across required areas:
Authentication
Authorization
Data Storage
API Communication
Logging & Monitoring
Administrative Access

2. Threat Model Table
| ID | STRIDE      | Threat Description                                | Affected Component         | Impact                                | Risk   |
| -- | ----------- | ------------------------------------------------- | -------------------------- | ------------------------------------- | ------ |
| T1 | Spoofing    | Credential stuffing attack using leaked passwords | Auth Service               | Account takeover, fraudulent payments | High   |
| T2 | Spoofing    | Session hijacking via stolen token                | API Gateway / Web Frontend | Unauthorized transaction execution    | High   |
| T3 | Repudiation | User denies initiating a transaction              | Transaction Service        | Dispute handling difficulty           | Medium |

Risk Reasoning:
High likelihood (credential reuse common)
High impact (financial loss)
Therefore High risk

AUTHORIZATION THREATS
| ID | STRIDE    | Threat Description                                                  | Affected Component | Impact                 | Risk |
| -- | --------- | ------------------------------------------------------------------- | ------------------ | ---------------------- | ---- |
| T4 | Elevation | Broken access control allows merchant to view other merchants’ data | Merchant Service   | Confidentiality breach | High |
| T5 | Elevation | Admin privilege escalation                                          | Admin Service      | Full system compromise | High |
| T6 | Tampering | Parameter tampering modifies refund amount                          | Payment Service    | Financial fraud        | High |

Risk Reasoning
Authorization failures directly enable fraud and financial manipulation

DATA STORAGE THREATS
| ID | STRIDE                 | Threat Description                              | Affected Component               | Impact                  | Risk |
| -- | ---------------------- | ----------------------------------------------- | -------------------------------- | ----------------------- | ---- |
| T7 | Information Disclosure | Database breach exposes PII and transactions    | User / Merchant / Transaction DB | Massive data breach     | High |
| T8 | Tampering              | Unauthorized modification of transaction ledger | Transaction DB                   | Financial inconsistency | High |
| T9 | Information Disclosure | Secrets exposed in source code or config        | Secrets Store                    | System-wide compromise  | High |

Risk Reasoning
Databases contain financial + personal data lead to severe regulatory + financial impact

API COMMUNICATION THREATS
| ID  | STRIDE                 | Threat Description                         | Affected Component | Impact                           | Risk |
| --- | ---------------------- | ------------------------------------------ | ------------------ | -------------------------------- | ---- |
| T10 | Information Disclosure | No TLS → traffic sniffing                  | Client ↔ API       | Credential leakage               | High |
| T11 | Tampering              | Man-in-the-middle modifies payment request | API Gateway        | Incorrect transaction processing | High |
| T12 | Denial of Service      | API flooding attack                        | API Gateway        | System downtime                  | High |

Risk Reasoning
System is internet-facing, high exposure. 

LOGGING & MONITORING THREATS
| ID  | STRIDE      | Threat Description              | Affected Component | Impact          | Risk |
| --- | ----------- | ------------------------------- | ------------------ | --------------- | ---- |
| T13 | Repudiation | Missing logs for admin actions  | Audit Logs         | No traceability | High |
| T14 | Tampering   | Attacker deletes or alters logs | Log Storage        | Fraud hidden    | High |

Risk Reasoning
Without logs, no forensic capability and compliance failure.

ADMINISTRATIVE ACCESS THREATS
| ID  | STRIDE            | Threat Description                | Affected Component   | Impact                 | Risk   |
| --- | ----------------- | --------------------------------- | -------------------- | ---------------------- | ------ |
| T15 | Spoofing          | Phishing attack against admin     | Admin Portal         | Full compromise        | High   |
| T16 | Elevation         | Lack of admin-user separation     | Network Architecture | Lateral movement       | High   |
| T17 | Denial of Service | Targeted DoS against admin portal | Admin Portal         | Operational disruption | Medium |

Risk Reasoning

Admin compromise = catastrophic impact is high

