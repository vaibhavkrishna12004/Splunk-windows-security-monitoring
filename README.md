# Splunk-windows-security-monitoring


Built a SIEM lab using Splunk Enterprise and Universal Forwarder to ingest and analyze Windows Event Logs. Implemented detection rules for failed logins, privilege escalation, and brute-force attacks, with custom SPL queries and dashboards.
plunk-windows-security-monitoring


SIEM workflow: log collection, forwarding, detection and visualization using Splunk



OVERVIEW

This project demonstrates how a basic SIEM environment can be built to monitor Windows security activity. The setup includes collecting logs from a Windows machine, forwarding them to a Splunk server, and analyzing authentication events to identify suspicious behavior.

The goal was to simulate how a SOC analyst monitors login activity and detects anomalies such as repeated failed login attempts.



TOOLS USED

Splunk Enterprise
Splunk Universal Forwarder
Windows Event Viewer
Kali Linux



SETUP

A Windows 10 virtual machine was used as the log source. Splunk Enterprise was installed on a Linux system, acting as the SIEM server.

The Universal Forwarder was installed on the Windows machine and configured to send logs to the Splunk server over port 9997.

After verifying connectivity, Windows Security logs were enabled and successfully ingested into Splunk.



LOG COLLECTION

Windows Event Logs were forwarded and indexed in Splunk.  The logs of the windows Event viewer and splunk matches thus, verifying the activity.

The main log source used:
WinEventLog:Security

Once configured, logs started appearing in Splunk search.

<img width="1920" height="1051" alt="Screenshot From 2026-04-14 12-37-35" src="https://github.com/user-attachments/assets/ce95bec5-b32a-4302-96ab-1e13ae2d0f5c" />


<img width="1024" height="768" alt="Logs detected" src="https://github.com/user-attachments/assets/c55bdda5-8543-4876-ae8f-b79d95d0f2fe" />

DETECTION

Using Splunk queries (SPL), authentication activity was analyzed.

Key Event IDs monitored:

4625 → Failed login attempts
4624 → Successful logins
4672 → Privileged (admin) logins

Example query used:

index=* EventCode=4625
| stats count by Account_Name
| where count > 5
<img width="1920" height="1051" alt="Screenshot From 2026-04-14 12-36-28" src="https://github.com/user-attachments/assets/cbb0c26c-d204-488f-b8ed-4cb4a6bc8fac" />



<img width="1024" height="768" alt="Event viewer log detection" src="https://github.com/user-attachments/assets/a993475d-942f-4ce3-9d5b-33626a31b528" />
<img width="1920" height="1051" alt="Screenshot From 2026-04-14 12-36-53" src="https://github.com/user-attachments/assets/6850c452-7b89-412d-b260-b6547b1a90df" />

<img width="1920" height="1051" alt="Screenshot From 2026-04-14 12-36-59" src="https://github.com/user-attachments/assets/eb816357-e708-495f-82ac-719b99c6e413" />






VISUALIZATION

A dashboard was created to visualize authentication activity.

It includes:

- Login distribution (success vs failure)
- Failed login attempts
- Privileged access events


<img width="1920" height="1051" alt="Screenshot From 2026-04-14 12-59-03" src="https://github.com/user-attachments/assets/abfb0dfb-81a5-46e7-bbc0-b05da72b4226" />



ANALYSIS

From the collected logs, it was possible to observe:

- Repeated failed login attempts within short time intervals
- Successful logins after multiple failures
- Administrative privilege usage

This reflects how real-world monitoring systems identify suspicious authentication patterns.



CONCLUSION

This project shows how logs from a Windows system can be centralized and analyzed using Splunk. By creating detection queries and dashboards, it becomes possible to monitor user activity and identify potential threats such as brute-force login attempts.

It highlights the importance of log monitoring and how SIEM tools help in detecting suspicious behavior in real environments.
