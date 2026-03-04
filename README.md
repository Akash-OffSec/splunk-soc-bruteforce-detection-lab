# SOC Monitoring & SSH Brute Force Detection Lab (Splunk SIEM)

## Overview
This project demonstrates detection of SSH brute force attacks using Splunk SIEM in a simulated SOC lab environment.

A Kali Linux attacker performs brute-force login attempts against an Ubuntu server. Authentication logs from the Ubuntu system are forwarded to Splunk Enterprise using the Splunk Universal Forwarder. The attack activity is analyzed, visualized, and detected using Splunk Search Processing Language (SPL).

---

## Lab Architecture

Kali Linux (Attacker)  
↓  
Ubuntu Server (Target)  
↓  
Splunk Universal Forwarder  
↓  
Splunk Enterprise SIEM  

---

## Attack Simulation

The Hydra password-cracking tool was used from Kali Linux to perform SSH brute-force login attempts against the Ubuntu server.

Example command used:

hydra -l root -P passwords.txt ssh://192.168.1.20

---

## Detection in Splunk

Authentication logs from `/var/log/auth.log` were analyzed in Splunk.

Example SPL query used for detection:

index=* host=aakash source="/var/log/auth.log" "Failed password"
| rex field=_raw "from (?<attacker_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by attacker_ip
| sort -count

---

## SOC Monitoring

A Splunk dashboard was created to visualize failed SSH login attempts and identify suspicious authentication activity.

A scheduled alert was also configured to detect abnormal spikes in failed login attempts, which can indicate brute-force attacks.

---

## Tools Used

- Splunk Enterprise  
- Splunk Universal Forwarder  
- Kali Linux  
- Ubuntu Server  
- Hydra  

---
## SOC Investigation

When the alert triggered, the analyst verified
authentication logs and identified the attacker IP.
The spike in failed SSH logins confirmed brute-force activity.

## Screenshots

Project screenshots including the lab architecture, attack simulation,
Splunk analysis, dashboard monitoring, and alert configuration are
available in the **attack-simulation** folder.

## Full Project Report

The complete project report with detailed setup steps, screenshots,
and analysis is available here:

Google Drive Report:
 (https://drive.google.com/file/d/1FHiBqEEXKUfOOd2Oaj9w8sWy3wXR71He/view?usp=drive_link)

## Author

Akash Sharma  
Cybersecurity | SOC Analyst | Security Monitoring
