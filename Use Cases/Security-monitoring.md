# 🛡️ Security Monitoring

## 📘 Overview

**Security Monitoring** is the continuous observation and analysis of systems, networks, applications, and security events to identify potential threats and investigate suspicious activity.

Security analysts use monitoring tools to detect unusual behavior, recognize indicators of compromise (IOCs), and determine whether an alert requires further investigation or incident response.

Security monitoring is a core activity in a **Security Operations Center (SOC)**, where analysts review alerts, correlate evidence, and help protect an organization's environment.

## 🎯 Objective

- Detect suspicious activity across systems and networks.
- Monitor authentication events and access attempts.
- Identify potential malware infections and unauthorized access.
- Correlate events from multiple security sources.
- Investigate alerts and distinguish genuine threats from false positives.
- Prioritize incidents based on likelihood and potential impact.
- Escalate confirmed or suspected incidents to the appropriate team.
- Maintain useful evidence for incident response and reporting.

## 🧠 Key Concepts

- **Security event:** An observable occurrence relevant to security, such as a login, firewall block, or process execution.
- **Security alert:** A notification generated when a rule or detection mechanism identifies potentially suspicious activity.
- **SIEM (Security Information and Event Management):** A platform that collects, normalizes, searches, and correlates logs to support detection and investigation.
- **IDS (Intrusion Detection System):** Detects suspicious activity and generates alerts.
- **IPS (Intrusion Prevention System):** Can block suspicious traffic when deployed inline and configured for prevention.
- **Log source:** A system or application that produces events, such as a firewall, server, endpoint, or identity provider.
- **Correlation:** Linking events from different sources to identify a broader pattern.
- **IOC (Indicator of Compromise):** An observable indicator associated with potentially malicious activity, such as a suspicious IP address, domain, or file hash.
- **Baseline:** A description of normal activity used to identify deviations.
- **False positive:** An alert that identifies legitimate activity as suspicious.
- **False negative:** Malicious activity that is not detected.
- **Triage:** The initial assessment used to determine an alert's relevance, urgency, and next steps.
- **Severity:** An assessment of how serious an event or alert may be.
- **Incident response:** The process of managing and addressing a security incident.
- **Playbook:** A documented procedure for investigating or responding to a particular type of alert.
- **Escalation:** Passing an alert or incident to a team with the appropriate responsibility or expertise.
- **MTTD (Mean Time to Detect):** The average time taken to detect an incident.
- **MTTR (Mean Time to Respond/Recover):** A metric used to measure response or recovery time; the precise definition depends on the organization.

## 🛠️ Tools Used

- **Logs / SIEM:** Centralizes and correlates events from multiple systems to help identify suspicious patterns.
- **IDS / Snort:** Detects network traffic matching configured rules and generates alerts.
- **Wireshark:** Examines packets and protocols to investigate network activity.
- **tcpdump:** Captures network traffic from the command line for focused analysis or later review.
- **CyberChef:** Decodes or transforms extracted data when an analyst needs to inspect its format or content.
- **Nmap:** Can help authorized responders verify which hosts and services are reachable during an investigation, when appropriate.

Each tool contributes a different type of evidence. A SIEM may reveal the pattern, Snort may flag the traffic, and Wireshark or tcpdump may help the analyst examine the underlying network communications.

## 🔎 Workflow

### Collect and monitor events

Collect logs and alerts from relevant sources, such as:

- Authentication systems.
- Servers and endpoints.
- Firewalls and network devices.
- DNS services.
- IDS/IPS platforms.
- Applications and cloud services.

Confirm that the sources are reporting correctly and that timestamps are sufficiently synchronized to compare events.

### Detect suspicious activity

Review alerts and detection rules for patterns such as:

- Repeated failed login attempts.
- A successful login following many failures.
- Unexpected administrative activity.
- Unusual outbound network connections.
- Communication with known malicious infrastructure.
- Unexpected changes to critical files or configurations.
- Alerts from multiple systems involving the same host or user.

A single event may have a legitimate explanation. Context and correlation are essential.

### Triage the alert

Establish:

- What triggered the alert?
- Which user, host, or service is involved?
- When did the event occur?
- Is the activity expected for this environment?
- Are there related alerts or events?
- What is the potential impact if the activity is malicious?

Prioritize alerts according to the available evidence, potential impact, and organizational procedures.

### Investigate supporting evidence

Search related logs and, when relevant, inspect network traffic.

For example, if a SIEM reports repeated connections to a suspicious destination, use Wireshark or tcpdump to examine available packet captures and determine which protocols and hosts were involved.

If Snort generated the alert, review the rule, packet details, and surrounding traffic to understand why it matched.

### Determine the next action

Depending on the evidence and the organization's procedures, the analyst may:

- Close the alert as a documented false positive.
- Continue monitoring for additional evidence.
- Escalate the investigation.
- Follow an approved incident-response playbook.
- Request containment or remediation by the authorized response team.

Do not isolate systems, disable accounts, or block network traffic unless the action is authorized and appropriate to the incident.

### Document the investigation

Record the alert source, timestamps, affected assets, relevant log entries, investigation steps, conclusions, and any escalation or response actions.

A good record should distinguish confirmed observations from hypotheses.

## 📋 Practical Examples

### Example 1 — Possible brute-force attack

The SIEM reports a large number of failed authentication attempts against one account.

The analyst checks the source IP, targeted account, time range, and authentication logs. They then determine whether a successful login followed the failures.

**Possible explanation:** A brute-force attempt, a misconfigured application, or a legitimate user repeatedly entering an incorrect password.

**Next step:** Correlate the evidence and follow the organization's authentication-incident procedure.

### Example 2 — Suspicious outbound traffic

An endpoint generates repeated outbound connections to an unfamiliar destination.

The analyst reviews DNS, firewall, endpoint, and SIEM records. If packet captures are available, they inspect the traffic with Wireshark.

**Goal:** Determine whether the connections are expected application behavior or potentially related to malicious activity.

### Example 3 — Investigating an IDS alert

Snort generates an alert for a known suspicious traffic pattern.

The analyst checks the signature, source and destination addresses, affected service, and packet details. They correlate the alert with endpoint logs to determine whether there is evidence of a successful compromise.

**Goal:** Validate the alert and assess whether further incident response is necessary.

### Example 4 — Unexpected administrative activity

A privileged account performs an unusual action outside its normal usage pattern.

The analyst reviews identity logs, the source device, timestamps, and any associated changes to systems or accounts.

**Goal:** Determine whether the activity was authorized, misconfigured, or potentially indicative of account compromise.

### Example 5 — Missing logs from a critical system

A critical server stops sending events to the SIEM.

The analyst checks the collection agent, connectivity, permissions, configuration, and source system status.

**Goal:** Restore monitoring visibility and determine whether the missing data affects an ongoing investigation.

## ⚠️ Important

- An alert is a signal to investigate, not proof that an attack succeeded.
- The absence of alerts does not prove that a system is secure.
- Monitoring quality depends on log coverage, detection rules, data quality, and analyst interpretation.
- Incorrect timestamps can make related events appear unrelated.
- Encrypted network traffic limits what a passive network sensor can inspect.
- Detection rules may produce false positives or miss threats.
- Preserve relevant evidence and follow organizational policies for log access, retention, and privacy.
- Use approved procedures for containment and remediation; unnecessary response actions can disrupt legitimate business activity.
- Effective monitoring combines technology, context, documented procedures, and human analysis.

## 📚 References

- NIST Computer Security Incident Handling Guide: https://csrc.nist.gov/pubs/sp/800/61/r2/final
- NIST Guide to Computer Security Log Management: https://csrc.nist.gov/pubs/sp/800/92/final
- Microsoft Sentinel documentation: https://learn.microsoft.com/en-us/azure/sentinel/
- Splunk documentation: https://docs.splunk.com/
- Snort documentation: https://docs.snort.org/
- Wireshark documentation: https://www.wireshark.org/docs/

## 🔗 Related Repository Files

- `logs-and-siem.md`
- `ids-and-snort.md`
- `wireshark.md`
- `tcpdump.md`
- `cyberchef.md`
- `network-traffic-analysis.md`
