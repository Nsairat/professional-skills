# Fintech Architecture & Security

## Fintech System Components

### Payment Processing Pipeline

```
Customer → Checkout → Payment Gateway → Processor → Card Network → Issuing Bank
                            ↓
                     Internal Ledger
                            ↓
                    Reconciliation
```

**Key Components**:
1. **Payment Gateway**: Tokenization, routing, 3DS authentication
2. **Payment Processor**: Clearing, settlement, merchant services
3. **Internal Ledger**: Double-entry accounting, transaction records
4. **Reconciliation**: Match internal records with bank statements

### Ledger Design Principles

**Double-Entry Accounting**:
- Every transaction has debit and credit entries
- Sum of debits = Sum of credits (always)
- Immutable entries; corrections via reversing entries
- Audit trail for every change

**Ledger Schema**:
```
Account
- id, account_type, currency, created_at

Transaction
- id, timestamp, description, idempotency_key

Entry
- id, transaction_id, account_id, amount, direction (DEBIT/CREDIT)
```

**Account Types**:
- Asset accounts (increase with debits)
- Liability accounts (increase with credits)
- Equity accounts
- Revenue/Expense accounts

---

### Fraud Detection System

**Real-Time Signals**:
- Device fingerprint anomalies
- Velocity checks (transactions per hour/day)
- Geolocation inconsistencies
- Behavioral biometrics
- Amount patterns

**Rule Engine Components**:
- Real-time rules (sub-100ms decisions)
- ML models (risk scoring)
- Manual review queue
- Feedback loop for model training

**Actions**:
- Allow, Decline, Step-up authentication
- 3DS challenge
- Manual review hold
- Account freeze

---

### KYC/AML Pipeline

**Identity Verification Steps**:
1. Document collection (ID, proof of address)
2. Document verification (authenticity check)
3. Biometric matching (selfie to ID photo)
4. Watchlist screening (OFAC, PEP lists)
5. Risk scoring and decisioning

**Ongoing Monitoring**:
- Transaction monitoring for suspicious patterns
- Periodic re-verification
- SAR (Suspicious Activity Report) filing
- Customer risk re-scoring

**Vendor Ecosystem**:
- Document verification: Jumio, Onfido, Veriff
- Watchlist screening: ComplyAdvantage, Dow Jones
- Transaction monitoring: Feedzai, NICE Actimize

---

## Compliance Frameworks

### PCI-DSS Requirements

**Level 1 Merchant** (>6M transactions/year):
- Annual on-site audit by QSA
- Quarterly network scans
- Penetration testing

**Key Requirements**:
| Requirement | Summary |
|-------------|---------|
| 1-2 | Firewall and secure configurations |
| 3 | Protect stored cardholder data |
| 4 | Encrypt transmission |
| 5-6 | Malware protection, secure development |
| 7-8-9 | Access control |
| 10 | Logging and monitoring |
| 11 | Regular testing |
| 12 | Security policies |

**Scope Reduction Strategies**:
- Tokenization (never store real PANs)
- Hosted payment pages (shift PCI scope to processor)
- P2PE (Point-to-Point Encryption)

---

### SOC 2 Type II

**Trust Service Criteria**:
1. **Security**: Protection against unauthorized access
2. **Availability**: System uptime commitments
3. **Processing Integrity**: Accurate processing
4. **Confidentiality**: Data protection
5. **Privacy**: PII handling

**Common Controls**:
- Access management and provisioning
- Change management
- Incident response
- Business continuity
- Vendor management
- Encryption standards

**Audit Process**:
- 6-12 month observation period
- Evidence collection throughout
- Auditor testing and interviews
- Report with findings and remediation

---

### GDPR / CCPA

**Key Rights**:
- Right to access (data export)
- Right to deletion (erasure requests)
- Right to portability
- Right to opt-out of sale (CCPA)

**Technical Requirements**:
- Data inventory and mapping
- Consent management system
- Subject access request workflow
- Data retention policies
- Privacy-by-design in development

---

## Security Architecture

### Zero Trust Principles

1. **Never trust, always verify**: Authenticate every request
2. **Least privilege**: Minimum access necessary
3. **Assume breach**: Design for compromise containment
4. **Verify explicitly**: User, device, location, data sensitivity

**Implementation**:
- Identity-based access (no network-based trust)
- Multi-factor authentication everywhere
- Micro-segmentation
- Continuous verification
- Encrypted communications (mTLS)

---

### Authentication & Authorization

**Authentication Patterns**:
- OAuth 2.0 / OpenID Connect for user authentication
- API keys for service-to-service (internal)
- JWT tokens with short expiry
- Refresh token rotation
- MFA enforcement by risk level

**Authorization Patterns**:
- RBAC (Role-Based Access Control) for simple cases
- ABAC (Attribute-Based) for complex policies
- Policy-as-code (Open Policy Agent)
- Centralized authorization service

---

### Data Protection

**Encryption at Rest**:
- AES-256 for stored data
- Key management via HSM or KMS
- Envelope encryption pattern
- Key rotation policies

**Encryption in Transit**:
- TLS 1.3 (minimum TLS 1.2)
- Certificate management and rotation
- Certificate pinning for mobile apps
- mTLS for service-to-service

**Tokenization**:
- Replace sensitive data with non-reversible tokens
- Token vault stores mapping securely
- Reduces PCI scope significantly
- Format-preserving for compatibility

**Data Masking**:
- Mask PII in non-production environments
- Reversible vs irreversible masking
- Dynamic masking for support access

---

### Application Security

**Secure Development Lifecycle**:
1. Security requirements in design
2. Threat modeling for new features
3. Secure coding guidelines
4. SAST (Static Analysis) in CI
5. DAST (Dynamic Analysis) in staging
6. Dependency scanning (SCA)
7. Security review before launch
8. Penetration testing

**OWASP Top 10 Mitigations**:
| Risk | Mitigation |
|------|------------|
| Injection | Parameterized queries, input validation |
| Broken Auth | Session management, MFA, rate limiting |
| Sensitive Data Exposure | Encryption, tokenization, masking |
| XXE | Disable DTDs, use simple formats |
| Broken Access Control | Authorization checks, RBAC |
| Security Misconfiguration | Hardening, automated config |
| XSS | Output encoding, CSP headers |
| Insecure Deserialization | Integrity checks, avoid untrusted |
| Vulnerable Components | Dependency scanning, patching |
| Insufficient Logging | Audit logs, monitoring, alerting |

---

### Infrastructure Security

**Network Security**:
- VPC isolation with private subnets
- Security groups (whitelist approach)
- WAF for public endpoints
- DDoS protection (CloudFlare, AWS Shield)
- Network flow logging

**Container Security**:
- Minimal base images
- Non-root execution
- Image scanning in CI
- Runtime security monitoring
- Pod security policies/standards

**Secrets Management**:
- Never commit secrets to code
- Vault, AWS Secrets Manager, or similar
- Secret rotation automation
- Least-privilege secret access
- Audit logging for secret access

---

### Incident Response

**Incident Severity Levels**:
| Level | Impact | Response Time | Escalation |
|-------|--------|---------------|------------|
| SEV1 | Customer-facing outage | 15 min | Executive, all-hands |
| SEV2 | Major degradation | 30 min | VP Engineering |
| SEV3 | Minor impact | 2 hours | Engineering Manager |
| SEV4 | No user impact | Next business day | Team |

**Response Playbook**:
1. **Detect**: Alerting, customer reports, monitoring
2. **Triage**: Assess severity, assign incident commander
3. **Contain**: Stop the bleeding, minimize impact
4. **Eradicate**: Fix root cause
5. **Recover**: Restore normal operations
6. **Learn**: Postmortem within 48 hours

**Security Incident Specifics**:
- Preserve evidence (logs, memory dumps)
- Contain without alerting attacker
- Legal and PR coordination
- Regulatory notification requirements
- Customer communication plan

---

## Vendor Security Assessment

### Due Diligence Checklist

**Compliance**:
- [ ] SOC 2 Type II report (review exceptions)
- [ ] PCI-DSS compliance if handling card data
- [ ] GDPR/CCPA compliance documentation
- [ ] Insurance coverage (cyber liability)

**Technical Security**:
- [ ] Encryption standards (at rest, in transit)
- [ ] Access control and authentication
- [ ] Incident response plan
- [ ] Penetration test results
- [ ] Vulnerability management program

**Operational**:
- [ ] SLA commitments and history
- [ ] Business continuity / DR plan
- [ ] Data retention and deletion policies
- [ ] Subprocessor list and management

**Contractual**:
- [ ] Security obligations in contract
- [ ] Breach notification requirements
- [ ] Audit rights
- [ ] Termination data handling
