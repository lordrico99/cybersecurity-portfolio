# Incident Report – Website Compromise

**Organization:** YummyRecipesForMe.com  
**Incident Type:** Brute Force Attack & Malware Redirect  
**Status:** Resolved  

---

## Executive Summary

YummyRecipesForMe.com was compromised following a successful brute force attack on the administrative account. The attacker gained unauthorized access using default credentials, modified the website source code, and embedded malicious JavaScript that prompted users to download an executable file.

When executed, the file redirected users to a malicious domain (greatrecipesforme.com), resulting in malware distribution.

---

## Incident Background

Customers reported being prompted to download a file to access website content. After executing the file, users were redirected to another domain and experienced system performance degradation.

The website administrator was unable to access the admin panel due to credential changes made by the attacker.

---

## Investigation Process

- Incident escalated following confirmation of website compromise
- Sandbox environment established for safe malware analysis
- Network traffic captured using tcpdump
- Website interaction reproduced in controlled environment
- Executable download observed
- Browser redirect to malicious domain confirmed

---

## Technical Analysis

### Network Protocols Observed

| Protocol | Function |
|----------|----------|
| DNS (UDP/53) | Resolves domain names to IP addresses |
| TCP | Establishes reliable connection (3-way handshake) |
| HTTP (Port 80) | Transfers webpage content and malicious payload |
| JavaScript | Embedded malicious redirect script |

---

### Observed Network Activity (tcpdump)

1. DNS request for `yummyrecipesforme.com`
2. DNS response with IP address `203.0.113.22`
3. TCP three-way handshake over port 80
4. HTTP GET request for homepage
5. Malicious JavaScript prompts executable download
6. DNS request for `greatrecipesforme.com`
7. DNS response with IP `192.0.2.17`
8. HTTP connection established to malicious domain

---

## Root Cause

The compromise occurred due to:

- Default administrative password not changed
- No account lockout mechanism
- No brute force protection controls
- No multi-factor authentication (MFA)
- Lack of monitoring for repeated failed login attempts

---

## Impact

- Website integrity compromised
- Malware distributed to customers
- Reputational damage
- Potential exposure of user systems

---

## Remediation Actions

- Removed malicious JavaScript from source code
- Restored website from clean backup
- Reset all administrative credentials
- Coordinated with hosting provider
- Conducted malware analysis in sandbox environment

---

## Security Recommendations

To prevent brute force attacks in the future:

1. Enforce strong password policies
2. Remove default credentials immediately upon deployment
3. Implement account lockout after repeated failed login attempts
4. Deploy Multi-Factor Authentication (MFA)
5. Enable login rate limiting
6. Deploy a Web Application Firewall (WAF)
7. Implement centralized logging and SIEM monitoring for failed login attempts
8. Conduct periodic access reviews of administrative accounts

---

## Conclusion

This incident was the result of weak credential management and the absence of brute force protection controls. Network analysis confirmed that DNS and HTTP protocols were used to deliver malicious content after administrative compromise.

Implementing layered authentication controls and monitoring mechanisms will significantly reduce the likelihood of similar attacks in the future.
