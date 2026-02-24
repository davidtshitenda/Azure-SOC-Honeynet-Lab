# Azure-SOC-Honeynet-Lab
A live SOC environment built in Azure using Microsoft Sentinel to detect and analyse real-world cyber attacks

## Objective

In this lab I deployed a live honeynet in Microsoft Azure by configuring a deliberately vulnerable Windows virtual machine exposed to the public internet. The environment was integrated with Microsoft Sentinel via a Log Analytics workspace and Data Collection Rule to ingest and analyse real-world security events. I configured a brute force detection analytics rule mapped to the MITRE ATT&CK framework, built a geolocation watchlist for IP enrichment, and connected the environment to Microsoft Defender XDR. The objective was to simulate a real SOC environment, detect live attack activity through KQL queries and custom analytics rules, and develop hands-on experience with cloud-native SIEM tooling relevant to a Security Operations Analyst role

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
![NSG Rule](screenshots/Picture3.png)

## Security Configuration

### DANGER-AllowAll Inbound Rule

*The default RDP inbound rule was removed and replaced with a single permissive rule allowing all inbound traffic. This was a deliberate architectural decision to maximise the VM's exposure to the internet and generate real-world attack telemetry for analysis in Sentinel.*

![Allow All Rule](screenshots/Picture4.png)

![Configuration of Rule](screenshots/Picture5.png)

![Final](screenshots/Picture6.png)

### VM Deployment Confirmed
![Deployment Complete](screenshots/Picture7.png)

*All five resources deployed successfully — the virtual machine, network interface, public IP address, associated deployment, and the NSG — confirming the environment was fully provisioned and ready for configuration.*

## Troubleshooting — RDP vs Azure Bastion
![RDP Failure - Part 1](screenshots/Picture8.png)

![RDP Failure - Part 2](screenshots/Picture9.png)

*During this lab all tasks were completed using a corporate laptop so there were certain limitations when it came to administrative tasks hence the RDP connection failing. Azure Bastion was used as an alternative secure connection method via the browser.*

![Bastion Success - Part 1](screenshots/Picture10.png)

![Bastion Success - Part 2](screenshots/Picture11.png)

### Disabling Windows Firewall
![Firewall Disabled](screenshots/Picture12.png)

*Windows Defender Firewall was disabled for both private and public network profiles inside the VM. This ensures inbound traffic is not blocked at the OS level, allowing attack attempts to reach the machine and generate loggable authentication events.*

## SIEM Integration

### Log Analytics Workspace
![LAW Creation](screenshots/Picture13.png)

### Connecting VM to Sentinel via AMA
![Content Hub](screenshots/Picture14.png)

*The data connector status confirmed as connected and actively receiving events, with the ingestion graph showing log volume increasing over time. This validated that the DCR was successfully shipping Windows Security Events from the VM to the Log Analytics workspace.*

### Data Collection Rule
![DCR](screenshots/Picture15.png)

### GeoIP Watchlist
![Watchlist - Part 1](screenshots/Picture16.png)

![Watchlist - Part 2](screenshots/Picture17.png)

![Watchlist - Part 3](screenshots/Picture18.png)

## Detection Engineering

### Brute Force Analytics Rule
![Analytics Rule](screenshots/Picture21.png)

*The completed analytics rule runs every hour, looks back across the last hour of data, groups alerts into a single incident to reduce noise, and maps entity types to both the attacker IP address and the targeted account — mirroring how production SOC detection rules are structured.*

## Workbook creation for visual mapping
![Workbook - Part 1](screenshots/Picture19.png)

![Watchlist - Part 2](screenshots/Picture20.png)

![Watchlist - Part 2](screenshots/Picture32.png)

### MITRE ATT&CK Mapping — T1110 Brute Force
![MITRE Mapping](screenshots/Picture22.png)

### Rule Summary
![Rule Summary](screenshots/Picture23.png)

*The Review and Create summary confirms the rule name, MITRE ATT&CK Credential Access mapping, High severity, hourly run frequency, entity mapping for both IP address and account, and alert grouping — all validated before saving*

## Findings and Analysis

*Within 24 hours of deployment the VM was discovered by automated threat actors with no additional exposure beyond the permissive NSG rule. A total of 15 failed authentication attempts were recorded across 4 unique source IP addresses. The most notable finding was IP 167.220.196.182 specifically targeting the actual administrator account username rather than generic defaults, suggesting either prior reconnaissance or credential list usage. IP 5.191.246.197 attempted both Administrator and admin variants consistent with automated password spraying tools. All attempts were detected by the brute force analytics rule and surfaced as incidents in Microsoft Sentinel.*

![Findings - Part 1](screenshots/Picture33.png)

![Rule Summary](screenshots/Picture34.png)

![Rule Summary](screenshots/Picture35.png)

![Rule Summary](screenshots/Picture36.png)

## Lessons Learned

*This lab reinforced that internet-exposed infrastructure attracts automated attack traffic extremely rapidly, highlighting the importance of restrictive NSG policies in production environments. Building the detection rule from scratch gave me practical insight into how SOC teams tune analytics rules to balance detection sensitivity against alert fatigue. Working through real configuration challenges such as the corporate laptop RDP restriction developed my troubleshooting approach and introduced me to Azure Bastion as a secure administrative access solution*
