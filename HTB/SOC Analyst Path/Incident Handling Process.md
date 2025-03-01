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


The `detection & analysis` phase involves all aspects of detecting an incident, such as utilizing sensors, logs, and trained personnel. It also includes information and knowledge sharing, as well as utilizing context-based threat intelligence. Segmentation of the architecture and having a clear understanding of and visibility within the network are also important factors.

Threats are introduced to the organization via an infinite amount of attack vectors, and their detection can come from sources such as:

- An employee that notices abnormal behavior
- An alert from one of our tools (EDR, IDS, Firewall, SIEM, etc.)
- Threat hunting activities
- A third-party notification informing us that they discovered signs of our organization being compromised

---

It is highly recommended to create levels of detection by logically categorizing our network as follows.

- Detection at the network perimeter (using firewalls, internet-facing network intrusion detection/prevention systems, demilitarized zone, etc.)
- Detection at the internal network level (using local firewalls, host intrusion detection/prevention systems, etc.)
- Detection at the endpoint level (using antivirus systems, endpoint detection & response systems, etc.)
- Detection at the application level (using application logs, service logs, etc.)

## Initial Investigation

When a security incident is detected, you should conduct some initial investigation and establish context before assembling the team and calling an organization-wide incident response. Think about how information is presented in the event of an administrative account connecting to an IP address at HH:MM:SS. 
Without knowing what system is on that IP address and which time zone the time refers to, we may easily jump to a wrong conclusion about what this event is about. To sum up, we should aim to collect as much information as possible at this stage about the following:

- Date/Time when the incident was reported. Additionally, who detected the incident and/or who reported it?
- How was the incident detected?
- What was the incident? Phishing? System unavailability? etc.
- Assemble a list of impacted systems (if relevant)
- Document who has accessed the impacted systems and what actions have been taken. Make a note of whether this is an ongoing incident or the suspicious activity has been stopped
- Physical location, operating systems, IP addresses and hostnames, system owner, system's purpose, current state of the system
- (If malware is involved) List of IP addresses, time and date of detection, type of malware, systems impacted, export of malicious files with forensic information on them (such as hashes, copies of the files, etc.)

## Incident Severity & Extent Questions

When handling a security incident, we should also try to answer the following questions to get an idea of the incident's severity and extent:

- What is the exploitation impact?
- What are the exploitation requirements?
- Can any business-critical systems be affected by the incident?
- Are there any suggested remediation steps?
- How many systems have been impacted?
- Is the exploit being used in the wild?
- Does the exploit have any worm-like capabilities?
The last two can possibly indicate the level of sophistication of an adversary.

To leverage IOCs, we will have to deploy an IOC-obtaining/IOC-searching tool (native or third party and possibly at scale). A common approach is to utilize WMI or PowerShell for IOC-related operations in Windows environments. A word of caution! During an investigation, we have to be extra careful to prevent the credentials of our highly privileged user(s) from being cached when connecting to (potentially) compromised systems (or any systems, really). More specifically, we need to ensure that only connection protocols and tools that don't cache credentials upon a successful login are utilized (such as WinRM). Windows logons with logon type 3 (Network Logon) typically don't cache credentials on the remote systems. The best example of "know your tools" that comes to mind is "PsExec". When "PsExec" is used with explicit credentials, those credentials are cached on the remote machine. When "PsExec" is used without credentials through the session of the currently logged on user, the credentials are not cached on the remote machine. This is a great example of demonstrating how the same tool leaves different tracks, so be aware.

## Containment

In this stage, we take action to prevent the spread of the incident. We divide the actions into `short-term containment` and `long-term containment`. It is important that containment actions are coordinated and executed across all systems simultaneously. Otherwise, we risk notifying attackers that we are after them, in which case they might change their techniques and tools in order to persist in the environment.

In short-term containment, the actions taken leave a minimal footprint on the systems on which they occur. Some of these actions can include, placing a system in a separate/isolated VLAN, pulling the network cable out of the system(s) or modifying the attacker's C2 DNS name to a system under our control or to a non-existing one. The actions here contain the damage and provide time to develop a more concrete remediation strategy. Additionally, since we keep the systems unaltered (as much as possible), we have the opportunity to take forensic images and preserve evidence if this wasn't already done during the investigation (this is also known as the `backup` substage of the containment stage). If a short-term containment action requires shutting down a system, we have to ensure that this is communicated to the business and appropriate permissions are granted.

In long-term containment actions, we focus on persistent actions and changes. These can include changing user passwords, applying firewall rules, inserting a host intrusion detection system, applying a system patch, and shutting down systems. While doing these activities, we should keep the business and the relevant stakeholders updated. Bear in mind that just because a system is now patched does not mean that the incident is over. Eradication, recovery, and post-incident activities are still pending.

---

## Eradication

Once the incident is contained, eradication is necessary to eliminate both the root cause of the incident and what is left of it to ensure that the adversary is out of the systems and network. Some of the activities in this stage include removing the detected malware from systems, rebuilding some systems, and restoring others from backup. During the eradication stage, we may extend the previously performed containment activities by applying additional patches, which were not immediately required. Additional system-hardening activities are often performed during the eradication stage (not only on the impacted system but across the network in some cases).

---

## Recovery

In the recovery stage, we bring systems back to normal operation. Of course, the business needs to verify that a system is in fact working as expected and that it contains all the necessary data. When everything is verified, these systems are brought into the production environment. All restored systems will be subject to heavy logging and monitoring after an incident, as compromised systems tend to be targets again if the adversary regains access to the environment in a short period of time. Typical suspicious events to monitor for are:

- Unusual logons (e.g. user or service accounts that have never logged in there before)
- Unusual processes
- Changes to the registry in locations that are usually modified by malware

The recovery stage in some large incidents may take months, since it is often approached in phases. During the early phases, the focus is on increasing overall security to prevent future incidents through quick wins and the elimination of low-hanging fruits. The later phases focus on permanent, long-term changes to keep the organization as secure as possible.