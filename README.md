
# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- NTANetAnalytics (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/513ce396-5581-4241-b2a4-2dc62c097316" />


## Architecture After Hardening / Security Controls
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/935be622-98b1-4024-9e30-e26744cf0777" />


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
<img width="1606" height="672" alt="image" src="https://github.com/user-attachments/assets/873d6911-da55-441d-98d9-95051955082b" />
<br>
<img width="1557" height="756" alt="image" src="https://github.com/user-attachments/assets/ebc6c28c-def4-4b79-8359-6c99862f56a6" />
<br>
<img width="1585" height="717" alt="image" src="https://github.com/user-attachments/assets/867d4c2f-ad85-483c-b92f-6204c62c1e91" />


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time  2025-09-05T19:59:34
Stop Time  2025-09-06T19:59:34

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7912
| Syslog                   | 9978
| SecurityAlert            | 204
| SecurityIncident         | 298
| NTANetAnalytics          | 2247

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2025-09-08T22:55:56
Stop Time	2025-09-09T22:55:56

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 787
| Syslog                   | 4
| SecurityAlert            | 0
| SecurityIncident         | 0
| NTANetAnalytics          | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
