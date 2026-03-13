# SSH Log Analysis & Brute Force Detection using Splunk

## Overview

This project demonstrates how Security Operations Center (SOC) analysts investigate SSH authentication logs using Splunk to detect brute-force attacks, suspicious login attempts, and unauthorized access activity.

## Tools Used

* Splunk Enterprise
* Linux SSH Authentication Logs
* SPL (Search Processing Language)

## Log Ingestion

The SSH authentication logs were uploaded into Splunk for security analysis.

### Steps to Upload Logs into Splunk

1. Login to the Splunk Web Interface.
2. Navigate to **Settings → Add Data**.
3. Select **Upload** as the data input method.
4. Upload the file:

ssh_log.json

5. Set the **Source Type** to:

_json

6. Create or select the index:

ssh_logs

7. Review the data preview and complete the ingestion process.

After ingestion, the logs become searchable using **Splunk Search Processing Language (SPL)**.

## Log Fields Analyzed

The following fields were extracted and used during the investigation:

* **event_type** – Type of SSH activity (successful login, failed login, etc.)
* **auth_success** – Indicates whether authentication succeeded
* **auth_attempts** – Number of authentication attempts
* **id.orig_h** – Source IP address initiating the connection
* **id.resp_h** – Destination host receiving the SSH connection

## Security Use Cases Implemented

* Failed SSH login detection
* Brute-force authentication detection
* Successful login monitoring
* Detection of SSH connections without authentication
