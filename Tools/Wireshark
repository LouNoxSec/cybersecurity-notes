# 🛡️ Wireshark

## 📘 Overview

Wireshark is a network protocol analyzer used to capture and inspect network traffic at the packet level.

## 🎯 Purpose

- Analyze network communications.
- Troubleshoot connectivity problems.
- Identify protocols and communication patterns.
- Investigate suspicious network activity.
- Examine packet capture files (`.pcap`, `.pcapng`).

## 🧠 Key Concepts

- **Packet:** A unit of data transmitted over a network.
- **Protocol:** A set of rules governing communication between devices.
- **Capture filter:** Restricts which traffic is collected during a capture.
- **Display filter:** Selects which packets are displayed after capture.
- **Source IP:** The IP address of the device sending a packet.
- **Destination IP:** The IP address of the intended recipient.
- **Port:** Identifies a service or application endpoint.
- **TCP stream:** A reconstructed TCP conversation between endpoints.
- **PCAP:** A file format used to store captured network traffic.

## 💻 Commands / Operations

Wireshark is primarily a graphical application. Most analysis is performed through its interface and display filters.

**Useful display filters**

- DNS traffic: `dns`
- HTTP traffic: `http`
- TCP traffic: `tcp`
- ICMP traffic: `icmp`
- Traffic involving a specific IP: `ip.addr == 192.168.1.10`
- Traffic from a specific IP: `ip.src == 192.168.1.10`
- Traffic to a specific IP: `ip.dst == 192.168.1.20`
- Traffic using port 443: `tcp.port == 443`
- Traffic using DNS port 53: `udp.port == 53`
- TCP connection attempts: `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- TCP retransmissions: `tcp.analysis.retransmission`

**Basic workflow**

1. Open Wireshark.
2. Select the network interface to monitor.
3. Start capturing packets.
4. Generate or observe the traffic you want to investigate.
5. Apply a display filter.
6. Select a packet to inspect its protocol layers and fields.
7. Stop the capture and save it if necessary.

## 📋 Practical Examples

**Example 1 — Investigate DNS traffic**

Apply the display filter `dns`.

Inspect the queried domain, the DNS server, the response, and any error codes.

**Example 2 — Investigate a connectivity issue**

Apply `ip.addr == 192.168.1.10` to isolate traffic involving the device.

Check whether requests leave the device and whether responses return.

**Example 3 — Investigate TCP connection attempts**

Apply `tcp.flags.syn == 1 && tcp.flags.ack == 0`.

This displays initial TCP connection attempts. Repeated attempts without successful handshakes may indicate a connectivity problem, filtering, or an unavailable service.

## 🔎 Investigation

When analyzing a capture, check:

- Source and destination IP addresses.
- Source and destination ports.
- Protocols used.
- Request and response patterns.
- TCP retransmissions and connection failures.
- DNS queries and responses.
- Unexpected destinations or unusual traffic patterns.

**Useful investigation question:** Is the expected communication occurring, and does the destination respond as expected?

## ⚠️ Important

- A capture filter and a display filter serve different purposes.
- A display filter does not delete packets from the original capture.
- Encrypted HTTPS traffic generally does not reveal the HTTP application content without suitable decryption access.
- A single suspicious packet is not sufficient to prove malicious activity; investigate the surrounding context.
- Captured traffic may contain credentials, personal information, or other sensitive data.
- Capture and analyze traffic only on systems and networks you are authorized to monitor.

## 📚 References

- Official website: https://www.wireshark.org/
- User guide: https://www.wireshark.org/docs/wsug_html_chunked/
- Display filter reference: https://www.wireshark.org/docs/dfref/
