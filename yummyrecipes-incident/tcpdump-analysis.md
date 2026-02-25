# Incident Analysis – YummyRecipesForMe.com

## Part One: TCPDump Log Analysis

**Summary of the Problem:**

- Users could not access the website `www.yummyrecipesforme.com`.  
- TCPDump logs show multiple failed **DNS queries over UDP port 53**.  
- Each query received an **ICMP “udp port 53 unreachable”** error message.  

**Protocols Observed:**

| Protocol | Role in Network Traffic |
|----------|------------------------|
| UDP      | DNS queries to resolve domain names |
| ICMP     | Error reporting (“port unreachable”) |
| HTTPS    | Web browser attempted connection (TCP/443) |

**Key Log Entries:**

| Timestamp          | Source IP        | Destination IP      | Protocol | Info |
|-------------------|----------------|------------------|---------|------|
| 13:24:32.192571   | 192.51.100.15  | 203.0.113.2       | UDP     | DNS query for `yummyrecipesforme.com` |
| 13:24:32.192571   | 203.0.113.2    | 192.51.100.15     | ICMP    | udp port 53 unreachable |
| 13:28:32.192571   | 192.51.100.15  | 203.0.113.2       | UDP     | DNS query repeated |
| 13:28:32.192571   | 203.0.113.2    | 192.51.100.15     | ICMP    | udp port 53 unreachable |

**Interpretation:**

- **UDP port 53 is blocked or unavailable**, preventing DNS resolution.  
- HTTPS requests cannot reach the web server because the browser cannot resolve the domain name.  
- The ICMP error clearly indicates a **DNS service or network issue**.

---

## Part Two: Investigation & Resolution

**Incident Timeline:**

- **Reported:** Users could not access the website, receiving “destination port unreachable.”

**Scenario, Events, and Symptoms:**

- TCPDump shows the first incident occured at 1:24pm
- Multiple clients experienced website downtime.  
- Browser error: “destination port unreachable.”  
- TCPDump shows ICMP errors in response to DNS queries.

**Current Status:**

- DNS queries continue to fail.  
- Website remains inaccessible due to DNS resolution failure.  

**Investigation Findings:**

- DNS (UDP/53) is the affected protocol.  
- ICMP errors indicate **blocked/unreachable port 53**.  
- No HTTPS traffic reached the web server because IP resolution failed.

**Next Steps in Troubleshooting:**

1. Check DNS service status and restart if necessary.  
2. Verify firewall rules allow **UDP port 53**.  
3. Test DNS resolution from multiple clients or networks.  
4. Consider temporary alternative DNS for testing.  
5. Monitor logs to confirm resolution.

**Suspected Root Cause:**

- DNS server unreachable on UDP port 53 due to:  
  - Firewall blocking traffic  
  - DNS service stopped/misconfigured  
  - Network routing issue
  - Successful Denial of Service attack 

**Recommended Solution:**

- Restart DNS service and ensure **UDP port 53 is open** on all firewalls.  
- Test client access and website availability.  
- Implement centralized logging and Security Information and Event Management (SIEM) monitoring to detect and alert on DNS service disruptions or abnormal traffic patterns in real time.
- Deploy IDS/IPS and Harden Firewall rules to mitigate against possible DOS attacks
