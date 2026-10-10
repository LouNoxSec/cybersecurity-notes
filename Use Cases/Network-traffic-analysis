# 🛡️ Network Traffic Analysis

## 📘 Overview

**Network Traffic Analysis** is the process of capturing, inspecting, and interpreting network communications to understand how devices communicate and to identify suspicious or unexpected activity.

Security analysts use network traffic analysis to troubleshoot connectivity issues, investigate security alerts, identify potential attacks, and understand communication between hosts.

Traffic can be examined in real time or analyzed later using a packet capture file, commonly called a **PCAP**.

## 🎯 Objective

- Understand communication between network devices.
- Identify the source and destination of network connections.
- Examine protocols, ports, and packet contents when visible.
- Detect suspicious network behavior and potential indicators of compromise (IOCs).
- Investigate unusual DNS requests, unexpected connections, or repeated connection attempts.
- Correlate network evidence with logs and security alerts.
- Support incident response and network troubleshooting.

## 🧠 Key Concepts

- **Packet:** A unit of data transmitted across a network.
- **Packet capture (PCAP):** A file containing captured network traffic for later analysis.
- **Protocol:** A set of rules governing communication, such as TCP, UDP, DNS, HTTP, or TLS.
- **Source IP / Destination IP:** The IP addresses identifying the apparent sender and receiver of a packet at the observed network point.
- **Source port / Destination port:** Port numbers associated with the communicating applications or services.
- **TCP handshake:** The three-way process using SYN, SYN-ACK, and ACK to establish a TCP connection.
- **DNS query:** A request to resolve a domain name to information such as an IP address.
- **HTTP:** An application protocol used for web communication. Its contents may be readable when transmitted without encryption.
- **HTTPS / TLS:** Encrypted web communication that limits the visibility of application data to a passive observer.
- **Packet filtering:** Selecting packets based on conditions such as IP addresses, protocols, or ports.
- **Display filter:** A Wireshark filter that controls which captured packets are shown without deleting the underlying capture.
- **Capture filter:** A filter applied during capture to determine which packets are recorded.
- **IOC (Indicator of Compromise):** An indicator associated with potentially malicious activity, such as a suspicious IP address, domain, or file hash.
- **Baseline:** A representation of normal network behavior used to identify unusual activity.

## 🛠️ Tools Used

- **Wireshark:** Graphically inspects packets, protocols, and communication sequences.
- **tcpdump:** Captures and filters network packets from the command line.
- **Snort:** Detects traffic matching configured security rules and can generate alerts.
- **Logs / SIEM:** Correlates network-related events with authentication, endpoint, firewall, and other security logs.
- **CyberChef:** Decodes and transforms extracted data when its encoding or format is understood.

Each tool has a different role. Wireshark and tcpdump provide packet-level visibility, Snort performs rule-based detection, a SIEM helps correlate events across sources, and CyberChef assists with data transformations.

## 🔎 Workflow

### Identify the investigation scope

Determine which device, time period, network segment, or security alert needs to be investigated.

Clarify whether the objective is troubleshooting, threat detection, or incident investigation.

### Capture or obtain the traffic

Use an existing PCAP file or capture traffic from an authorized network observation point.

Example with tcpdump:

`sudo tcpdump -i eth0 -nn -w capture.pcap`

- `-i eth0`: Selects the network interface.
- `-nn`: Disables hostname and service-name resolution.
- `-w capture.pcap`: Writes captured packets to a file.

Replace `eth0` with the correct interface name for the environment. Capture only traffic you are authorized to monitor.

### Inspect the capture

Open the PCAP in Wireshark and examine:

- The protocols being used.
- Source and destination IP addresses.
- Source and destination ports.
- Connection establishment and termination.
- DNS queries and responses.
- Unusual packet patterns or repeated connection attempts.

### Apply display filters

Examples of useful Wireshark display filters:

- `dns` — Displays DNS packets.
- `tcp` — Displays TCP packets.
- `icmp` — Displays ICMP packets.
- `ip.addr == 192.168.1.10` — Displays IPv4 packets involving that address.
- `tcp.flags.syn == 1 && tcp.flags.ack == 0` — Displays TCP packets with SYN set and ACK not set, often associated with connection initiation.
- `tcp.port == 443` — Displays TCP packets involving port 443.

These filters narrow the displayed traffic; they do not, by themselves, prove that activity is malicious.

### Investigate suspicious patterns

Look for patterns such as:

- Many connection attempts to different ports on one host.
- Repeated failed or unanswered connection attempts.
- Unexpected outbound connections.
- DNS requests to suspicious or unusual domains.
- Communication with an IP address associated with a known threat.
- Traffic volume or timing that differs significantly from normal behavior.

Validate the context before classifying a pattern as malicious.

### Correlate the evidence

Compare the packet capture with relevant firewall logs, endpoint alerts, authentication records, and SIEM events.

Check whether the same host, user, destination, and time period appear across multiple sources.

### Document the findings

Record the relevant timestamps, IP addresses, ports, protocols, filters used, observations, and supporting evidence.

Clearly distinguish observed facts from hypotheses that still require validation.

## 📋 Practical Examples

### Example 1 — Investigating a suspicious DNS query

A workstation generates a DNS request for an unfamiliar domain.

The analyst filters for DNS traffic in Wireshark, identifies the querying host, examines the domain and response, and correlates the event with endpoint or SIEM logs.

**Goal:** Determine whether the request is legitimate, misconfigured, or potentially related to malicious activity.

### Example 2 — Investigating repeated connection attempts

A server receives repeated TCP SYN packets from one source, targeting multiple destination ports.

The analyst reviews the source address, target ports, timing, and connection responses.

**Possible explanation:** Port scanning, an authorized vulnerability scan, or another application behavior. More context is required to distinguish them.

### Example 3 — Troubleshooting a failed TCP connection

A user reports that an application cannot connect to a server.

The analyst checks whether TCP SYN packets are sent, whether SYN-ACK responses return, and whether the connection completes.

If SYN packets are repeatedly retransmitted without a response, possible causes include filtering, routing problems, an unavailable service, or a return-path issue.

**Goal:** Identify where the connection appears to fail and continue troubleshooting with supporting network evidence.

### Example 4 — Investigating an IDS alert

Snort generates an alert for traffic matching a suspicious rule.

The analyst locates the corresponding packets in Wireshark, reviews the rule details, and checks whether the traffic matches the expected pattern.

The analyst then correlates the event with endpoint and firewall logs to assess whether the alert represents a genuine threat.

**Goal:** Validate the alert and determine whether further investigation or response is necessary.

## ⚠️ Important

- A packet capture shows only the traffic visible at the capture point. It may not represent all communications on the network.
- Switched networks, VLANs, network TAPs, SPAN ports, routing, and capture-interface placement affect traffic visibility.
- Encrypted traffic, such as HTTPS, generally hides application payloads from passive inspection, although metadata may remain visible.
- A suspicious IP address, port, or domain is not sufficient by itself to prove malicious activity.
- A large number of TCP SYN packets may indicate scanning, but legitimate monitoring and application behavior can produce similar patterns.
- Capture filters and display filters serve different purposes: capture filters limit what is recorded; display filters limit what is shown.
- PCAP files may contain sensitive information. Handle, store, and share them according to applicable policies.
- Use authorized environments and preserve relevant evidence when investigating security incidents.

## 📚 References

- Wireshark documentation: https://www.wireshark.org/docs/
- Wireshark display filter reference: https://www.wireshark.org/docs/dfref/
- tcpdump manual: https://www.tcpdump.org/manpages/tcpdump.1.html
- Snort documentation: https://docs.snort.org/
- CyberChef: https://gchq.github.io/CyberChef/
- NIST Guide to Intrusion Detection and Prevention Systems: https://csrc.nist.gov/pubs/sp/800/94/final

## 🔗 Related Repository Files

- `wireshark.md`
- `tcpdump.md`
- `ids-and-snort.md`
- `logs-and-siem.md`
- `cyberchef.md`
