# Azure-SOC-Honeynet-Lab
A live SOC environment built in Azure using Microsoft Sentinel to detect and analyse real-world cyber attacks

In this lab I deployed a live honeynet in Microsoft Azure by configuring a deliberately vulnerable Windows virtual machine exposed to the public internet. The environment was integrated with Microsoft Sentinel via a Log Analytics workspace and Data Collection Rule to ingest and analyse real-world security events. I configured a brute force detection analytics rule mapped to the MITRE ATT&CK framework, built a geolocation watchlist for IP enrichment, and connected the environment to Microsoft Defender XDR. The objective was to simulate a real SOC environment, detect live attack activity through KQL queries and custom analytics rules, and develop hands-on experience with cloud-native SIEM tooling relevant to a Security Operations Analyst role

# Azure SOC Honeynet Lab

## Objective
*paste your objective paragraph here*

## Architecture
![Architecture Diagram](SOC-Honeynet-Architecture.svg)

## Technologies Used
- Microsoft Azure
- Microsoft Sentinel
- Log Analytics Workspace
- Windows Server 2022
- Azure Bastion
- Microsoft Defender XDR
- KQL (Kusto Query Language)
- CompTIA Security+ / SC-200 concepts applied

## Environment Setup

### VM Creation
![VM Creation](screenshots/Picture1.png)

*The Standard_D2ls_v5 size was selected after the B1s was unavailable in South Africa North for free tier subscriptions.*

![VM configuration](screenshots/Picture2.png)

### NSG Configuration  
![NSG Rule](screenshots/Picture2.png)

## Security Configuration

### DANGER-AllowAll Inbound Rule
![Allow All Rule](screenshots/Picture3.png)

*The default RDP inbound rule was removed and replaced with a single permissive rule allowing all inbound traffic. This was a deliberate architectural decision to maximise the VM's exposure to the internet and generate real-world attack telemetry for analysis in Sentinel.*

### VM Deployment Confirmed
![Deployment Complete](screenshots/Picture4.png)

*caption here*

## Troubleshooting — RDP vs Azure Bastion
![RDP Failure](screenshots/Picture5.png)

*During this lab all tasks were completed using a 
corporate laptop so there were certain limitations 
when it came to administrative tasks hence the RDP 
connection failing. Azure Bastion was used as an 
alternative secure connection method via the browser.*

![Bastion Success](screenshots/Picture6.png)

### Disabling Windows Firewall
![Firewall Disabled](screenshots/Picture7.png)
*caption here*

## SIEM Integration

### Log Analytics Workspace
![LAW Creation](screenshots/Picture8.png)
*caption here*

### Connecting VM to Sentinel via AMA
![Content Hub](screenshots/Picture9.png)
*caption here*

### Data Collection Rule
![DCR](screenshots/Picture10.png)
*caption here*

### GeoIP Watchlist
![Watchlist](screenshots/Picture11.png)
*caption here*

## Detection Engineering

### Brute Force Analytics Rule
![Analytics Rule](screenshots/Picture12.png)
*caption here*

### MITRE ATT&CK Mapping — T1110 Brute Force
![MITRE Mapping](screenshots/Picture13.png)
*caption here*

### Rule Summary
![Rule Summary](screenshots/Picture14.png)
*caption here*

## Findings and Analysis
*This section will be updated once attack data begins 
flowing into the workspace. The VM remains exposed 
with the DANGER-AllowAll rule active and logs are 
expected to populate within 24 hours.*

## Lessons Learned
*coming soon*
