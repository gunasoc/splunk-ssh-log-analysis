# SPL Queries – SSH Log Analysis

This document contains the **Splunk Search Processing Language (SPL)** queries used in the project to analyze SSH authentication logs and detect suspicious activities.

---

# 1. Log Ingestion Validation

Validate that logs are successfully ingested and categorized by event type.

```spl
index=ssh_logs
| stats count by event_type
```

Purpose:

* Verify log ingestion into Splunk
* Ensure event types are parsed correctly

---

# 2. Failed SSH Login Attempts

Identify failed SSH authentication attempts by source IP.

```spl
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h
| sort -count
```

Purpose:

* Detect systems attempting unauthorized SSH access
* Identify top attacking IP addresses

Visualization:

* Bar chart showing failed login attempts per IP

---

# 3. Top 10 Source IPs with Failed Logins

Highlight the most active IPs generating failed login attempts.

```spl
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h
| sort -count
| head 10
```

Purpose:

* Quickly identify potential brute force attackers
* Prioritize investigation of high-frequency login attempts

---

# 4. Detect Multiple Failed Authentication Attempts

Search for logs indicating multiple authentication failures.

```spl
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h, id.resp_h
```

Purpose:

* Detect brute-force attack behavior
* Identify attacker IP and target host

---

# 5. Detect Repeated Login Failures (Brute Force)

Identify IP addresses generating excessive login failures.

```spl
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h
| where count > 5
```

Purpose:

* Identify brute force login attempts
* Support alert generation in SOC monitoring

---

# 6. Successful SSH Login Activity

Monitor successful SSH authentication attempts.

```spl
index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h, id.resp_h
```

Purpose:

* Identify legitimate access patterns
* Detect suspicious successful logins after repeated failures

---

# 7. Compare Successful Logins After Failed Attempts

Investigate possible account compromise scenarios.

```spl
index=ssh_logs (event_type="Failed SSH Login" OR event_type="Successful SSH Login")
| stats count by id.orig_h, event_type
```

Purpose:

* Identify IPs that failed multiple times before succeeding
* Detect potential credential compromise

---

# 8. Unauthenticated SSH Connections

Detect SSH connections that were established without authentication.

```spl
index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h
```

Purpose:

* Identify SSH scanning attempts
* Detect reconnaissance activity

---

# 9. Monitor Unauthenticated Connections Over Time

Track repeated SSH probing behavior.

```spl
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
```

Purpose:

* Visualize attack trends over time
* Detect persistent scanning activity

---

# Summary

These queries simulate common SOC monitoring activities including:

* SSH brute force detection
* Login failure analysis
* Authentication monitoring
* Reconnaissance detection
* Security alert investigation

The queries demonstrate practical use of SPL for real-world security monitoring.
