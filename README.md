# Azure-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction
For this project, I constructed a small-scale honeynet within the Azure cloud platform. The objective was to collect log data from diverse sources and centralize it in a Log Analytics workspace. Subsequently, Microsoft Sentinel was employed to analyze the data and generate attack maps, raise alerts, and record security incidents. In the initial phase, I evaluated security metrics in the vulnerable environment for a period of 24 hours. Following that, I implemented security measures to fortify the environment and measured metrics for an additional 24 hours. The results of these assessments are presented below, focusing on the following metrics:





- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" measurements, all resources were initially deployed in a manner where they were directly exposed to the internet. This configuration allowed Virtual Machines to have both their Network Security Groups and built-in firewalls with unrestricted access. Additionally, all other resources were deployed with public endpoints visible to the internet, rendering Private Endpoints unnecessary.

On the other hand, for the "AFTER" metrics, significant security improvements were implemented. Network Security Groups were strengthened by blocking ALL traffic except for that originating from my admin workstation. Moreover, all other resources benefited from enhanced protection through their built-in firewalls as well as the use of Private Endpoints, ensuring a more secure and controlled environment.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/vdvfDNI.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/LArKr77.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/fXbEsXC.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-07-21 15:10:30
Stop Time 2023-07-22 15:10:30

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 84418
| Syslog                   | 4716
| SecurityAlert            | 5
| SecurityIncident         | 311
| AzureNetworkAnalytics_CL | 1065

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

For this project, we set up a small-scale honeynet on Microsoft Azure, integrating various log sources into a Log Analytics workspace. Microsoft Sentinel was utilized to analyze the logs, generating alerts and recording incidents based on the data collected. As part of the assessment, we measured metrics in the vulnerable environment before implementing security controls. After applying these measures, we re-evaluated the metrics, witnessing a significant reduction in the number of security events and incidents. This outcome serves as evidence of the effectiveness of the security controls.

Furthermore, it is important to consider that if the network resources were extensively used by regular users, there could have been an increase in security events and alerts during the 24-hour period after implementing the security controls.
