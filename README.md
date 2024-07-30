# Azure Honeynet and SOC with Real-World Cyber Attacks
![Cloud Honeynet / SOC](https://imgur.com/uAAcV74.png)

## Introduction and Objective

In this project, a mini honeynet was constructed on the Azure platform. The objective was to capture and analyze logs from various sources, which were then consolidated within a Log Analytics workspace. Microsoft Sentinel was deployed to utilize these logs by developing attack maps, creating alert triggers, and generating incidents. Azure Sentinel measured the metrics of an insecure environment over a 24-hour period. Following this initial phase, security controls were implemented to strengthen the virtual environment. Another 24-hour metric measurement phase was then conducted. The results from these efforts are presented below. The metrics analyzed were:

SecurityEvent: Windows Event Logs
Syslog: Linux Event Logs
SecurityAlert: Log Analytics Alerts Triggered
SecurityIncident: Incidents created by Sentinel
AzureNetworkAnalytics_CL: Malicious Flows allowed into our honeynet

## Technologies, Azure Components, and Regulations Employed

- Azure Virtual Network (VNet)
- Azure Network Security Groups (NSG)
- Virtual Machines: 2 Windows VMs, 1 Linux VM
- Log Analytics Workspace: Utilizing Kusto Query Language (KQL) Queries
- Azure Key Vault: For Secure Secrets Management
- Azure Storage Account: For Data Storage
- Microsoft Sentinel: For Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud: To Protect Cloud Resources
- Windows Remote Desktop: For Remote Access
- Command Line Interface (CLI): For System Management
- PowerShell: For Automation and Configuration Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

## Methodology

- <b>Creating the Honeynet:</b> I started by [deploying multiple vulnerable virtual machines](https://github.com/sindycp/Azure-VM-Setup) in Azure to simulate an insecure environment.

- <b>Monitoring and Analysis:</b> Azure was configured to ingest logs from various resources into a Log Analytics workspace. Microsoft Sentinel was used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>Security Metrics Measurement:</b> The environment was observed for 24 hours, recording key security metrics in its insecure state. This provided a baseline for comparison after implementing remediation measures.

- <b>Incident Response and Remediation:</b> After addressing the incidents and identifying vulnerabilities, I hardened the environment by applying security best practices and Azure-specific recommendations.

- <b>Post-Remediation Analysis:</b> The environment was observed again for another 24 hours to measure security metrics, comparing the results with the initial baseline.


## Architecture Before Hardening and Implementing Security Controls
![Architecture Diagram](https://imgur.com/ZDvrrNP.png)

During the "BEFORE" stage of the project, [a virtual environment was deployed ](https://github.com/sindycp/Azure-VM-Setup) and exposed to the public to attract malicious actors and observe their attack patterns. To achieve this, a Windows virtual machine hosting a SQL database and a Linux server were deployed with their network security groups (NSGs) configured to allow all traffic. To further entice attackers, a storage account and key vault were deployed with public endpoints visible on the open internet. Throughout this stage, the unsecured environment was monitored by Microsoft Sentinel using logs aggregated by the Log Analytics workspace.

## Architecture After Hardening and Implementing Security Controls

![Architecture Diagram](https://imgur.com/rBHH2sX.png)

During the "AFTER" stage of the project, the environment was hardened and security controls were implemented to improve the environment's overall security posture. These hardening tactics included:

- Network Security Groups (NSGs): NSGs were configured to block all inbound and outbound traffic except for designated public IP addresses requiring access to the virtual machines. This ensured that only authorized traffic from trusted sources could access the virtual machines.

- Built-in Firewalls: Azure's built-in firewalls were configured on the virtual machines to restrict unauthorized access and protect resources from malicious connections. This involved fine-tuning firewall rules based on the service and responsibilities of each VM, mitigating the attack surface available to malicious actors.

- Private Endpoints: Public endpoints for Azure Key Vault and Storage Containers were replaced with private endpoints. This limited access to these sensitive resources to within the virtual network, removing their exposure to the public internet.

## Attack Maps Before Hardening / Security Controls

<b>This attack map illustrates the consequences of leaving the Network Security Group (NSG) open, allowing malicious traffic to flow unimpeded. It highlights the critical importance of implementing proper security measures, such as restricting NSG rules, to prevent unauthorized access and minimize potential threats.</b>
  
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/NUtUoMe.png)<br>

<b>This attack map highlights the numerous syslog authentication failures experienced by the deployed Linux server, indicating unauthorized access attempts from external sources. It serves as a reminder of the importance of securing Linux servers with strong authentication mechanisms and monitoring system logs for signs of intrusion attempts.</b>

![Linux Syslog Auth Failures](https://i.imgur.com/RPkzsFc.png?1)<br>

<b>This attack map showcases numerous RDP and SMB failures, illustrating persistent attempts by potential attackers to exploit these protocols. This visualization underscores the necessity of securing remote access and file sharing services to protect against unauthorized access and potential cyber threats.</b>

![Windows RDP/SMB Auth Failures](https://i.imgur.com/ypIGuwx.png)<br>

## Attack Maps After Hardening / Security Controls

> All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

 ## Metrics Before Hardening / Security Controls
The following table shows the metrics measured within the unsecured environment for 24 hours:
Start Time 2024-07-24 17:17:10
Stop Time 2024-07-25 17:17:10

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 73331
| Syslog (Linux VM)                   | 3952
| SecurityAlert (Microsoft Defender for Cloud)            | 39
| SecurityIncident (Sentinel Incidents)        | 48
| NSG Inbound Malicious Flows Allowed | 1670

## Metrics After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

The following table shows the metrics measured in the environment for another 24 hours after applying security controls:
Start Time 2024-07-27 18:52:43
Stop Time	2024-07-28 18:52:43

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 1344
| Syslog (Linux VM)                   | 22
| SecurityAlert (Microsoft Defender for Cloud)            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion

This project involved creating an efficient mini honeynet in Microsoft Azure, integrating log sources into a Log Analytics workspace. Microsoft Sentinel was set up to generate alerts and incidents based on these logs. Metrics were collected both before and after applying security controls. After implementing enhanced security measures, there was a significant decrease in security events: a 98% reduction in Windows Security Events, a 99% reduction in Linux Events, and a complete 100% elimination of security alerts, incidents, and malicious inbound network traffic.
