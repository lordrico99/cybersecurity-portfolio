# Internal Audit – Controls and Compliance Checklist

**Company:** Botium Toys  
**Reference:** Scope, Goals, and Risk Assessment

---

## Controls Assessment

| Control | In Place? (Yes/No) | Notes |
|---------|------------------|------|
| Least Privilege | No | Employees can access sensitive data |
| Disaster Recovery Plans | No | No formal DR plan; critical data not backed up |
| Password Policies | No | Weak policy, not centrally enforced |
| Separation of Duties | No | Not implemented |
| Firewall | Yes | Configured and monitored |
| Intrusion Detection System (IDS) | No | Not implemented |
| Backups | No | No regular backups |
| Antivirus Software | Yes | Installed and monitored |
| Manual Monitoring, Maintenance for Legacy Systems | Partial | Monitored but no schedule |
| Encryption | No | Cardholder and sensitive data not encrypted |
| Password Management System | No | No centralized system |
| Locks (offices, storefront, warehouse) | Yes | Physical access controls implemented |
| CCTV Surveillance | Yes | Monitored |
| Fire Detection / Prevention | Yes | Functional |

---

## Compliance Checklist

### PCI DSS

| Best Practice | Compliant? | Notes |
|---------------|------------|------|
| Only authorized users have access to card data | No | All employees currently have access |
| Card info securely stored, transmitted, processed | No | No encryption applied |
| Implement data encryption procedures | No | Not implemented |
| Adopt secure password management policies | No | Weak and unenforced |

### GDPR

| Best Practice | Compliant? | Notes |
|---------------|------------|------|
| E.U. customers’ data kept private/secured | Partial | Policies exist but not fully enforced |
| 72-hour breach notification plan | Yes | Notification plan exists |
| Properly classify and inventory data | No | Asset inventory incomplete |
| Enforce privacy policies, procedures, processes | Partial | Policies exist; adherence gaps |

### SOC 1 & 2

| Best Practice | Compliant? | Notes |
|---------------|------------|------|
| User access policies established | Partial | Policies exist but enforcement weak |
| Sensitive data (PII/SPII) confidential | No | No encryption; all employees have access |
| Data integrity maintained | Yes | Controls in place |
| Data available to authorized users | Yes | Operational access exists |
