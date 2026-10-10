# 🛡️ IDS and Snort

## 📘 Overview

An **IDS (Intrusion Detection System)** monitors network traffic or system activity to identify suspicious behavior, potential attacks, and policy violations.

**Snort** is an open-source network security tool that can operate as an IDS, an IPS (Intrusion Prevention System), or a packet logger, depending on its configuration and deployment.

An IDS generally detects and alerts. An IPS can also block or prevent detected activity when deployed inline and configured to do so.

## 🎯 Purpose

- Monitor network traffic for suspicious activity.
- Detect known attack patterns and potential policy violations.
- Generate alerts for security analysts.
- Help investigate suspicious connections and network behavior.
- Support incident response and security monitoring.
- Identify potential threats such as scans, exploit attempts, and certain malware-related traffic.

## 🧠 Key Concepts

- **IDS (Intrusion Detection System):** Detects suspicious activity and generates alerts but does not normally block traffic.
- **IPS (Intrusion Prevention System):** Can block or prevent suspicious traffic when deployed inline and configured appropriately.
- **NIDS (Network IDS):** Monitors network traffic, typically at a network observation point.
- **HIDS (Host IDS):** Monitors activity on an individual system, such as system logs, files, or processes.
- **Signature-based detection:** Matches traffic or activity against known patterns and rules.
- **Anomaly-based detection:** Identifies behavior that deviates from an established baseline or expected behavior.
- **False positive:** Legitimate activity incorrectly identified as suspicious.
- **False negative:** Malicious activity that the detection system fails to identify.
- **Rule / Signature:** A definition describing traffic or behavior that should trigger an alert or action.
- **Packet inspection:** Examining packet headers and, where available and permitted, packet contents.
- **Promiscuous mode:** Allows a network interface to receive packets visible to it beyond those addressed specifically to that interface; it does not automatically make all network traffic on a switched network visible.
- **Inline deployment:** Places a security device directly in the traffic path, enabling an IPS to block traffic.
- **Out-of-band deployment:** Observes a copy of traffic, such as through a network TAP or SPAN port, without sitting directly in the forwarding path.

## 💻 Commands / Operations

These examples use Snort command-line options. Exact options and rule syntax can vary by Snort version; Snort 2 and Snort 3 are not fully interchangeable.

**Check the installed version**

`snort -V`

Displays version information.

**Test the configuration**

`snort -T -c /etc/snort/snort.conf`

Tests the configuration file at the specified path. The path may differ by operating system and installation.

**Run Snort against a network interface**

`sudo snort -i eth0 -c /etc/snort/snort.conf`

Starts Snort using interface `eth0` and the specified configuration. Interface names and configuration paths depend on the environment.

**Read a packet capture**

`snort -r capture.pcap -c /etc/snort/snort.conf`

Processes a saved packet capture using the specified configuration and rules.

**Create a simple alert rule**

`alert icmp any any -> $HOME_NET any (msg:"ICMP traffic detected"; sid:1000001; rev:1;)`

This illustrative Snort 2-style rule generates an alert for matching ICMP traffic directed toward the configured home network. It requires the appropriate rule configuration and variable definitions to be loaded.

**Understand the rule fields**

- `alert`: Generate an alert when the rule matches.
- `icmp`: Match ICMP traffic.
- `any any`: Match any source IP and source port.
- `->`: Match traffic moving in the specified direction.
- `$HOME_NET any`: Match destinations within the configured home network and any destination port.
- `msg`: Text displayed with the alert.
- `sid`: Rule identifier; locally created Snort rules conventionally use IDs of `1000000` or higher.
- `rev`: Rule revision number.

## 📋 Practical Examples

**Example 1 — Detecting a network scan**

An IDS detects repeated connection attempts to multiple ports on one host.

The analyst examines the source IP, destination ports, timestamps, and related firewall logs to determine whether the activity is legitimate scanning or a potential attack.

**Example 2 — Detecting a known exploit pattern**

A Snort signature matches traffic associated with a known exploit attempt.

The analyst checks the alert details, affected destination, relevant packets, and whether the target system is vulnerable. A signature match is evidence to investigate, not automatic proof that exploitation succeeded.

**Example 3 — Understanding IDS vs IPS**

An IDS observes a suspicious packet and generates an alert while allowing the network traffic to continue.

An inline IPS may drop the packet if its rules, operating mode, and configuration instruct it to block the traffic.

**Example 4 — Investigating a false positive**

A legitimate application generates traffic that matches a detection rule.

The analyst validates the traffic, reviews the rule conditions, and adjusts the detection carefully if necessary, while preserving protection against genuine threats.

## 🔎 Investigation

When investigating a Snort alert:

- **Identify the signature:** Review the rule ID, message, and detection logic.
- **Identify the endpoints:** Examine source and destination IP addresses and ports.
- **Check the protocol:** Determine whether the event involves TCP, UDP, ICMP, or another protocol.
- **Review the packets:** Use packet captures and tools such as Wireshark when available.
- **Correlate events:** Compare the alert with firewall logs, endpoint telemetry, and SIEM data.
- **Validate the threat:** Determine whether the traffic represents an attack attempt, successful exploitation, or legitimate activity.
- **Assess the impact:** Identify affected systems and decide whether escalation or containment is required.

## ⚠️ Important

- An IDS detects suspicious activity; it does not normally block traffic.
- An IPS can prevent traffic when deployed inline and configured for prevention.
- Signature-based detection is effective for known patterns but may miss new or modified attacks.
- Anomaly-based detection can identify unusual behavior but may generate more false positives.
- Encrypted traffic limits what a network IDS can inspect unless appropriate visibility is available.
- A network IDS can only inspect traffic it can actually observe. Network TAPs, SPAN ports, interface placement, and network architecture affect visibility.
- Snort requires suitable rules and configuration to detect the activity of interest.
- Alerts should be validated using additional evidence before concluding that a system has been compromised.

## 📚 References

- Snort official website: https://www.snort.org/
- Snort documentation: https://docs.snort.org/
- Snort rules documentation: https://docs.snort.org/rules/
- CISA: https://www.cisa.gov/
