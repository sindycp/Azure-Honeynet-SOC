# Azure Honeynet and SOC with Real-World Cyber Attacks
![Cloud Honeynet / SOC](https:)

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
- NIST SP 800-53 Revision 5: For Security Controls
- NIST SP 800-61 Revision 2: For Incident Handling Guidance

## Methodology

- <b>Creating the Honeynet:</b> I started by deploying multiple vulnerable virtual machines in Azure to simulate an insecure environment.

- <b>Monitoring and Analysis:</b> Azure was configured to ingest logs from various resources into a Log Analytics workspace. Microsoft Sentinel was used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>Security Metrics Measurement:</b> The environment was observed for 24 hours, recording key security metrics in its insecure state. This provided a baseline for comparison after implementing remediation measures.

- <b>Incident Response and Remediation:</b> After addressing the incidents and identifying vulnerabilities, I hardened the environment by applying security best practices and Azure-specific recommendations.

- <b>Post-Remediation Analysis:</b> The environment was observed again for another 24 hours to measure security metrics, comparing the results with the initial baseline.


