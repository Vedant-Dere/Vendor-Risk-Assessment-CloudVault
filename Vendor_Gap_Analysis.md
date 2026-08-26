# Third-Party Vendor Risk Assessment: Gap Analysis
**Target Vendor:** CloudVault Inc.
**Assessor:** Vedant Dere
**Date:** August 2026
**Framework Alignment:** SOC 2 (Security, Availability, Confidentiality) & ISO 27001

## Executive Summary
A preliminary security documentation review was conducted on CloudVault Inc. to determine their suitability as a SaaS vendor for handling our internal PII. The review identified several Critical and High-risk control gaps across Identity Management, Cryptography, and Incident Response. 

## Identified Control Exceptions (Gap Analysis)

### 1. Identity & Access Management (IAM)
* **Control Gap:** Multi-Factor Authentication (MFA) is not enforced for database administrators or support engineers, and is delayed until Q4. 
* **Business Risk:** [CRITICAL] Compromise of a single administrator password could lead to a catastrophic data breach. 
* **Required Remediation:** Vendor must enforce MFA for all privileged access immediately before contract signing.

### 2. Cryptography & Data Protection
* **Control Gap:** Data in transit is permitted over TLS 1.0. 
* **Business Risk:** [CRITICAL] TLS 1.0 is a deprecated, fundamentally insecure protocol vulnerable to downgrade attacks (e.g., POODLE). Interception of customer PII is possible.
* **Required Remediation:** Vendor must disable TLS 1.0/1.1 and enforce TLS 1.2 or 1.3 exclusively.

### 3. Incident Response & Logging
* **Control Gap A (Notification):** Incident response policy promises customer notification 30 days *after* an investigation concludes.
* **Business Risk:** [HIGH] This violates global privacy laws (GDPR/CCPA) which mandate notification within 72 hours of discovery. We would face massive regulatory fines.
* **Control Gap B (Logging):** Audit logs are retained for only 14 days.
* **Required Remediation:** Update SLA to 72-hour breach notification. Implement cold-storage log retention for a minimum of 1 year to support forensic investigations.

### 4. Vulnerability Management
* **Control Gap:** Independent penetration testing has not been performed in over two years.
* **Business Risk:** [HIGH] Automated quarterly scans do not detect business logic flaws. The application's current attack surface is unknown.
* **Required Remediation:** Vendor must provide a clean letter of attestation from a 3rd-party penetration test conducted within the last 12 months.

### 5. Disaster Recovery & Availability
* **Control Gap:** Database backups for a cloud service are stored on a local, on-premise server.
* **Business Risk:** [MEDIUM] Violates cloud disaster recovery best practices. A physical disaster at the vendor's office could result in permanent loss of our customer data.
* **Required Remediation:** Implement encrypted, geographically isolated cloud backups (e.g., AWS S3 Cross-Region Replication).

### 6. Human Resources Security
* **Control Gap:** Background checks are limited only to staff with physical server room access.
* **Business Risk:** [MEDIUM] Remote engineers with logical access to PII are entirely unvetted, posing an insider threat risk.
* **Required Remediation:** Formal background checks must be mandatory for all employees prior to granting logical system access.
