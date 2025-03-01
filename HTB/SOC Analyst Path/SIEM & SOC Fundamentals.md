## Roles Within A SOC

A SOC team consists of diverse roles responsible for handling the continuous, operational aspect of enterprise information security. These roles may encompass:

- `SOC Director`: Responsible for overall management and strategic planning of the SOC, including budgeting, staffing, and alignment with organizational security objectives.
- `SOC Manager`: Oversees day-to-day operations, manages the team, coordinates incident response efforts, and ensures smooth collaboration with other departments.
- `Tier 1 Analyst`: Monitors security alerts and events, triages potential incidents, and escalates them to higher tiers for further investigation.
- `Tier 2 Analyst`: Performs in-depth analysis of escalated incidents, identifies patterns and trends, and develops mitigation strategies to address security threats.
- `Tier 3 Analyst`: Provides advanced expertise in handling complex security incidents, conducts threat hunting activities, and collaborates with other teams to improve the organization's security posture.
- `Detection Engineer`: A Detection Engineer is responsible for developing, implementing, and maintaining detection rules and signatures for security monitoring tools, such as SIEM, IDS/IPS, and EDR solutions. They work closely with security analysts to identify gaps in detection coverage and continuously improve the organization's ability to detect and respond to threats.
- `Incident Responder`: Takes charge of active security incidents, carries out in-depth digital forensics and containment and remediation efforts, and collaborates with other teams to restore affected systems and prevent future occurrences.
- `Threat Intelligence Analyst`: Gathers, analyzes, and disseminates threat intelligence data to help SOC team members better understand the threat landscape and proactively defend against emerging risks.
- `Security Engineer`: Develops, deploys, and maintains security tools, technologies, and infrastructure, and provides technical expertise to the SOC team.
- `Compliance and Governance Specialist`: Ensures that the organization's security practices and processes adhere to relevant industry standards, regulations, and best practices, and assists with audit and reporting requirements.
- `Security Awareness and Training Coordinator`: Develops and implements security training and awareness programs to educate employees about cybersecurity best practices and promote a culture of security within the organization.

## How To Build SIEM Use Cases

- Comprehend your needs, risks, and establish alerts for monitoring all necessary systems accordingly.
- Determine the priority and impact, then map the alert to the kill chain or MITRE framework.
- Establish the Time to Detection (TTD) and Time to Response (TTR) for the alert to assess the SIEM's effectiveness and analysts' performance.
- Create a Standard Operating Procedure (SOP) for managing alerts.
- Outline the process for refining alerts based on SIEM monitoring.
- Develop an Incident Response Plan (IRP) to address true positive incidents.
- Set Service Level Agreements (SLAs) and Operational Level Agreements (OLAs) between teams for handling alerts and following the IRP.
- Implement and maintain an audit process for managing alerts and incident reporting by analysts.
- Create documentation to review the logging status of machines or systems, the basis for creating alerts, and their triggering frequency.
- Establish a knowledge base document for essential information and updates to case management tools.

To define TTD and TTR, we need to focus on the rule's execution interval and the data ingestion pipeline discussed earlier. For this example, we set the rule to run every five minutes, monitoring all incoming logs.

When creating an SOP and documenting alert handling, consider the following:

- process.name
- process.parent.name
- event.action
- machine where the alert was detected
- user associated with the machine
- user activity within +/- 2 days of the alert's generation
- After gathering this information, defenders should engage with the user and examine the user's machine to analyze system logs, antivirus logs, and proxy logs from the SIEM for full visibility.

## What Is The Ideal Triaging Process?

1. `Initial Alert Review`:

- Thoroughly review the initial alert, including metadata, timestamp, source IP, destination IP, affected systems, and triggering rule/signature.
- Analyze associated logs (network traffic, system, application) to understand the alert's context.

1. `Alert Classification`:

- Classify the alert based on severity, impact, and urgency using the organization's predefined classification system.

1. `Alert Correlation`:

- Cross-reference the alert with related alerts, events, or incidents to identify patterns, similarities, or potential indicators of compromise (IOCs).
- Query the SIEM or log management system to gather relevant log data.
- Leverage threat intelligence feeds to check for known attack patterns or malware signatures.

1. `Enrichment of Alert Data`:

- Gather additional information to enrich the alert data and gain context:
    - Collect network packet captures, memory dumps, or file samples associated with the alert.
    - Utilize external threat intelligence sources, open-source tools, or sandboxes to analyze suspicious files, URLs, or IP addresses.
    - Conduct reconnaissance of affected systems for anomalies (network connections, processes, file modifications).

1. `Risk Assessment`:

- Evaluate the potential risk and impact to critical assets, data, or infrastructure:
    - Consider the value of affected systems, sensitivity of data, compliance requirements, and regulatory implications.
    - Determine likelihood of a successful attack or potential lateral movement.

1. `Contextual Analysis`:

- The analyst considers the context surrounding the alert, including the affected assets, their criticality, and the sensitivity of the data they handle.
- They evaluate the security controls in place, such as firewalls, intrusion detection/prevention systems, and endpoint protection solutions, to determine if the alert indicates a potential control failure or evasion technique.
- The analyst assesses the relevant compliance requirements, industry regulations, and contractual obligations to understand the implications of the alert on the organization's legal and regulatory compliance posture.

1. `Incident Response Planning`:

- Initiate an incident response plan if the alert is significant:
    - Document alert details, affected systems, observed behaviors, potential IOCs, and enrichment data.
    - Assign incident response team members with defined roles and responsibilities.
    - Coordinate with other teams (network operations, system administrators, vendors) as necessary.

1. `Consultation with IT Operations`:

- Assess the need for additional context or missing information by consulting with IT operations or relevant departments:
    - Engage in discussions or meetings to gather insights on the affected systems, recent changes, or ongoing maintenance activities.
    - Collaborate to understand any known issues, misconfigurations, or network changes that could potentially generate false-positive alerts.
    - Gain a holistic understanding of the environment and any non-malicious activities that might have triggered the alert.
    - Document the insights and information obtained during the consultation.

1. `Response Execution`:

- Based on the alert review, risk assessment, and consultation, determine the appropriate response actions.
- If the additional context resolves the alert or identifies it as a non-malicious event, take necessary actions without escalation.
- If the alert still indicates potential security concerns or requires further investigation, proceed with the incident response actions.

1. `Escalation`:

- Identify triggers for escalation based on organization's policies and alert severity:
    - Triggers may include compromise of critical systems/assets, ongoing attacks, unfamiliar/sophisticated techniques, widespread impact, or insider threats.
- Assess the alert against escalation triggers, considering potential consequences if not escalated.
- Follow internal escalation process, notifying higher-level teams/management responsible for incident response.
- Provide comprehensive alert summary, severity, potential impact, enrichment data, and risk assessment.
- Document all communication related to escalation.
- In some cases, escalate to external entities (law enforcement, incident response providers, CERTs) based on legal/regulatory requirements.

1. `Continuous Monitoring`:

- Continuously monitor the situation and incident response progress.
- Maintain open communication with escalated teams, providing updates on developments, findings, or changes in severity/impact.
- Collaborate closely with escalated teams for a coordinated response.

1. `De-escalation`:

- Evaluate the need for de-escalation as the incident response progresses and the situation is under control.
- De-escalate when the risk is mitigated, incident is contained, and further escalation is unnecessary.
- Notify relevant parties, providing a summary of actions taken, outcomes, and lessons learned.

Regularly review and update the process, aligning it with organizational policies, procedures, and guidelines. Adapt the process to address emerging threats and evolving needs.