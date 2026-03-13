# SSH Log Analysis & Brute Force Detection using Splunk

## Overview
This project demonstrates how Security Operations Center (SOC) analysts investigate SSH authentication logs using Splunk to detect brute-force attacks, suspicious login attempts, and unauthorized access activity.

## Tools Used
- Splunk Enterprise
- Linux SSH Authentication Logs
- SPL (Search Processing Language)

## Log Fields Analyzed
- event_type
- auth_success
- auth_attempts
- id.orig_h (source IP)
- id.resp_h (destination host)

## Security Use Cases Implemented

1. Failed SSH login detection
2. Brute-force authentication attempts
3. Successful login monitoring
4. Unauthenticated SSH connections detection
