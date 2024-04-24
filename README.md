# Building a SOC + Honeynet in Azure (Live Traffic)

## Introduction

I designed this project to emulate a honeynet in Azure that ingests log sources from a series of resources into the Log Analytics workspace to then be used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. Prior to the honeynet's launch, I measured security metrics in the unsecured environment for a 24 hour period before applying security controls in order to harden the environment. I then measured metrics for an additional 24 hours and have displayed the results below. The below metrics will include: 

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

Prior to any hardening used in the honeynet environment all resources were originally created and deployed without any protections, thus exposing them to the internet. All virtual machines deployed had their Network Security Groups and built-in firewalls disabled as well as all other deployed resources having public endpoints exposed to the internet. 

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

The section portraying metrics after hardening include Network Security Groups that were hardened to block all traffic with the exception of the administrator workstation. All other resources were hardened by configuring their respective firewalls as well as Private Endpoint. 

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/nL9wwba.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/BM6oTv5.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/6SclYhe.png)<br>
![MSSQL Auth Failures](https://i.imgur.com/6V0mNFQ.png)<br>
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:<br>
Start Time 2023-08-28<br>
Stop Time 2023-08-29<br>

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 113623
| Syslog                   | 866
| SecurityAlert            | 13
| SecurityIncident         | 344
| AzureNetworkAnalytics_CL | 3507


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:<br>
Start Time 2023-09-01<br>
Stop Time	2023-09-02<br>

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9608
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project has shown the honeynet constructed within Microsoft Azure and log sources integrated into Log Analytics Workspace in order to trigger alerts and create incidents based on ingested logs Microsoft Sentinel was deployed. Metrics were captured prior to securing the environment and then captured once more after implementation of hardening techniques. As seen between the before and after metrics it can be concluded that a drastic reduction in security incidents and events can be observed, thus demonstrating the effectiveness of the controls applied.  
