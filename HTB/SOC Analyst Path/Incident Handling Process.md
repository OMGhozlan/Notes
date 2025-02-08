**Event Definition**

An event can be defined as a specific occurrence within a system or network that triggers a reaction or response. It is often used to describe the activation of a particular process or action.

**Example Events**

*   A user sending an email: This could trigger a notification to the recipient's email client.
*   A mouse click: This can initiate a GUI (Graphical User Interface) interaction with the application.
*   A firewall allowing a connection request: This event may lead to the establishment of a (in)secure network connection.

**Event Characteristics**

Events typically have certain characteristics that define them. These include:

*   **Trigger**: The event is triggered by an action or condition within the system.
*   **Reaction**: The event triggers a response or reaction from the system or network.
*   **Duration**: Events can be transient (short-lived) or persistent, depending on their nature.

**Event Types**

There are different types of events that occur in various contexts:

*   System events: These occur within a specific system and may include tasks like starting a service or loading an application.
*   Network events: These happen when there is communication between devices on a network.
*   User events: These occur when users interact with the system, such as logging in or sending data.

**Incident Definition

An **incident** is a type of event that has a negative consequence. Examples of incidents include:

*   System crashes
*   Unauthorized access to sensitive data

Incidents can also occur due to external factors such as natural disasters or power failures.

What is classified as an **IT security incident** is varies between organizations, and therefore does not have a single definition . An **IT security incident** can be defined as **an event with a clear intent to cause harm that is performed against a computer system**. 

**Example (IT) Incidents**

- Data theft
- Funds theft
- Unauthorized access to data
- Installation and usage of malware and remote access tools

**Key Differences**

(Some of) the key differences between events and incidents are:

*   **Consequence**: Events can be positive or negative, while incidents always have a negative consequence.
*   **Trigger**: Both events and incidents are triggered by an action or condition within the system.
*   **Reaction**: While both events and incidents trigger a reaction, incidents often lead to more severe consequences.

`Incident handling is a clearly defined set of procedures to manage and respond to security incidents in a computer or network environment.`


Incident handling has two main activities, which are `investigating` and `recovering`

The investigation phase aims to:

*   Identify the initial "patient zero" victim and create an ongoing incident timeline
*   Determine the tools and malware used by the adversary
*   Document the compromised systems and the adversary's actions

Following the investigation, the `recovery` activity involves creating and implementing a recovery plan. When the plan is implemented, the business should resume normal operations if the incident caused any disruptions.

When an incident is fully handled, a report is issued that details the cause and cost of the incident. Additionally, "lessons learned" activities are performed to understand what the organization can do to prevent similar incidents from occurring again in the future.


## Preparation Prerequisites

During the preparation, we need to ensure that we have:

- Skilled incident handling team members (incident handling team members can be outsourced, but a basic capability and understanding of incident handling are necessary in-house regardless)
- Trained workforce (as much as possible, through security awareness activities or other means of training)
- Clear policies and documentation
- Tools (software and hardware)

## Clear Policies & Documentation

Some of the written policies and documentation should contain an up-to-date version of the following information:

- Contact information and roles of the incident handling team members
- Contact information for the legal and compliance department, management team, IT support, communications and media relations department, law enforcement, internet service providers, facility management, and external incident response team
- Incident response policy, plan, and procedures
- Incident information sharing policy and procedures
- Baselines of systems and networks, out of a golden image and a clean state environment
- Network diagrams
- Organization-wide asset management database
- User accounts with excessive privileges that can be used on-demand by the team when necessary (also to business-critical systems, which are handled with the skills needed to administer that specific system). These user accounts are normally enabled when an incident is confirmed during the initial investigation and then disabled once it is over. A mandatory password reset is also performed when disabling the users.
- Ability to acquire hardware, software, or an external resource without a complete procurement process (urgent purchase of up to a certain amount). The last thing you need during an incident is to wait for weeks for the approval of a $500 tool.
- Forensic/Investigative cheat sheets

## Tools (Software & Hardware)

Moving forward, we also need to ensure that we have the right tools to perform the job. These include, but are not limited to:

- Additional laptop or a forensic workstation for each incident handling team member to preserve disk images and log files, perform data analysis, and investigate without any restrictions (we know malware will be tested here, so tools such as antivirus should be disabled). These devices should be handled appropriately and not in a way that introduces risks to the organization.
- Digital forensic image acquisition and analysis tools
- Memory capture and analysis tools
- Live response capture and analysis
- Log analysis tools
- Network capture and analysis tools
- Network cables and switches
- Write blockers
- Hard drives for forensic imaging
- Power cables
- Screwdrivers, tweezers, and other relevant tools to repair or disassemble hardware devices if needed
- Indicator of Compromise (IOC) creator and the ability to search for IOCs across the organization
- Chain of custody forms
- Encryption software
- Ticket tracking system
- Secure facility for storage and investigation
- Incident handling system independent of your organization's infrastructure

## Endpoint Hardening (& EDR)

CIS and Microsoft baselines offer valuable guidance on endpoint hardening best practices. However, it's essential to note that each organization may have unique requirements and constraints that necessitate customizing these standards to meet specific needs.

Some key actions that can be taken to improve endpoint hardening include:

- Disable LLMNR/NetBIOS
- Implement [LAPS](https://techcommunity.microsoft.com/blog/itopstalkblog/step-by-step-guide-how-to-configure-microsoft-local-administrator-password-solut/2806185) and remove administrative privileges from regular users
- Disable or configure PowerShell in [ConstrainedLanguage](https://devblogs.microsoft.com/powershell/powershell-constrained-language-mode/) mode
- Enable [Attack Surface Reduction](https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction)  (ASR) rules if using Microsoft Defender
- Implement whitelisting. We know this is nearly impossible to implement. Consider at least blocking execution from user-writable folders (Downloads, Desktop, AppData, etc.). These are the locations where exploits and malicious payloads will initially find themselves. Remember to also block script types such as .hta, .vbs, .cmd, .bat, .js, and similar. Please pay attention to [LOLBin](https://lolbas-project.github.io/) files while implementing whitelisting. Do not overlook them; they are really used in the wild as initial access to bypass whitelisting.
- Utilize host-based firewalls. As a bare minimum, block workstation-to-workstation communication and block outbound traffic to LOLBins
- Deploy an EDR product. At this point in time, [AMSI](https://learn.microsoft.com/en-us/windows/win32/amsi/how-amsi-helps) provides great visibility into obfuscated scripts for antimalware products to inspect the content before it gets executed. It is highly recommended that you only choose products that integrate with AMSI.

## Network Protection


*   Network segmentation is a powerful technique to avoid having a breach spread across the entire organization.
*   Business-critical systems must be isolated, and connections should be allowed only as the business requires.
*   Internal resources should not face the Internet directly (unless placed in a DMZ).
*   IDS/IPS systems can identify malicious traffic based on content on the wire, rather than relying on reputation of IP addresses.
*   Solutions like 802.1x can reduce the risk of BYOD or malicious devices connecting to the corporate network.
*   Conditional Access policies can achieve similar protection in cloud-only companies using Azure/Azure AD (Entra ID).

## Privilege Identity Management / MFA / Passwords

Here are the bullet points summarizing the information:

*   Stealing privileged user credentials is a common escalation path in Active Directory environments.
*   Admin users often have weak or shared passwords, which can be easily obtained through various attack vectors.
*   Weak but complex passwords, such as "Password1!", are vulnerable to prediction and brute-force attacks despite their complexity.
*   Teaching employees to use passphrases is recommended for additional protection. Passphrases like "i LIK3 my coffeE warm" are easy to remember yet long and complex. Using langauges can also help "F1yL1k3@T@ub3"
*   Implementing multi-factor authentication (MFA) at least for administrative access to all applications and devices is an effective way to protect identities.

## Vulnerability Scanning

- Perform continuous vulnerability scans of your environment.
- Remediate at least the "high" and "critical" vulnerabilities discovered during scanning.
- While automated scanning is possible, manual involvement is often required to apply patches or fixes.
- If patching cannot be done, vulnerable systems should be known and segmented

## User Awareness Training

Training users to recognize suspicious behavior and report it when discovered is a big win for us. While it is unlikely to reach 100% success on this task, these trainings are known to significantly reduce the number of successful compromises. Periodic "surprise" testing should also be part of this training, including, for example, monthly phishing emails, dropped USB sticks in the office building, etc.