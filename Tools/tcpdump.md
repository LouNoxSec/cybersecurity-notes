# 🛡️ tcpdump

## 📘 Overview

tcpdump is a command-line packet analyzer used to capture, filter, and inspect network traffic.

It is commonly used on Linux systems and servers where a graphical interface may not be available.

## 🎯 Purpose

- Capture network packets in real time.
- Troubleshoot connectivity and communication problems.
- Investigate DNS, TCP, UDP, and ICMP traffic.
- Identify communication between hosts.
- Save network captures for later analysis with tools such as Wireshark.

## 🧠 Key Concepts

- **Packet:** A unit of data transmitted across a network.
- **Network interface:** The adapter through which traffic is captured, such as `eth0` or `ens33`.
- **Capture filter:** A condition that determines which packets tcpdump captures.
- **BPF (Berkeley Packet Filter):** The filtering mechanism used by tcpdump.
- **PCAP:** A file format commonly used to store captured packets.
- **Promiscuous mode:** A mode that allows an interface to receive frames beyond those addressed specifically to it, where supported by the network and interface configuration.
- **Root privileges:** Administrative permissions often required to capture packets.

## 💻 Commands / Operations

**List available interfaces**

`sudo tcpdump -D`

Displays the interfaces available for packet capture.

**Capture traffic on a specific interface**

`sudo tcpdump -i eth0`

Replace `eth0` with the actual interface name on your system.

**Capture ICMP traffic**

`sudo tcpdump -i eth0 icmp`

Useful for observing ping requests and replies.

**Capture DNS traffic**

`sudo tcpdump -i eth0 port 53`

Captures traffic using port 53, commonly associated with DNS.

**Capture traffic involving a specific host**

`sudo tcpdump -i eth0 host 192.168.1.10`

Displays packets to or from the specified IP address.

**Capture traffic on a specific port**

`sudo tcpdump -i eth0 port 443`

Captures traffic involving TCP or UDP port 443.

**Display IP addresses and ports numerically**

`sudo tcpdump -nn -i eth0`

The `-nn` option prevents tcpdump from resolving IP addresses and port numbers into names.

**Limit the number of captured packets**

`sudo tcpdump -i eth0 -c 20`

Stops after capturing 20 packets.

**Save a capture to a file**

`sudo tcpdump -i eth0 -w capture.pcap`

Writes captured packets to a file for later analysis.

**Read a saved capture**

`tcpdump -r capture.pcap`

Reads packets from an existing capture file.

**Display packet contents in ASCII**

`sudo tcpdump -A -i eth0`

Displays packet contents as ASCII where possible. Use caution because captured data may be sensitive.

## 📋 Practical Examples

**Example 1 — Investigate a DNS problem**

Run `sudo tcpdump -i eth0 port 53`.

Look for outgoing DNS queries and corresponding responses. Repeated queries without replies may indicate a DNS server, routing, or filtering problem.

**Example 2 — Check ICMP communication**

Run `sudo tcpdump -i eth0 icmp` while performing a ping test.

Look for echo requests and echo replies to determine whether ICMP traffic is visible on the monitored interface.

**Example 3 — Save traffic for further analysis**

Run `sudo tcpdump -i eth0 -w investigation.pcap`.

Open the resulting file in Wireshark to inspect packets and apply more advanced display filters.

## 🔎 Investigation

When examining captured traffic, check:

- Source and destination IP addresses.
- Source and destination ports.
- Protocols and packet frequency.
- Requests that receive no responses.
- TCP retransmissions or repeated connection attempts.
- Unexpected destinations or unusual communication patterns.

**Useful investigation question:** Is traffic reaching the expected destination, and is the destination responding?

Remember that tcpdump only observes traffic visible to the selected interface. A missing packet in the capture does not automatically prove that the packet was never sent.

## ⚠️ Important

- Interface names vary by operating system; use `tcpdump -D` to identify available interfaces.
- Administrative privileges may be required.
- Capture filters determine what is collected, so an overly restrictive filter may exclude useful evidence.
- The `-w` option saves packets to a file; it does not display their decoded contents in the terminal.
- Encrypted traffic may be captured, but encryption generally prevents inspection of its application content without appropriate decryption access.
- Packet captures can contain credentials, personal information, and other sensitive data.
- Capture traffic only on systems and networks you are authorized to monitor.

## 📚 References

- Official website: https://www.tcpdump.org/
- Manual page: https://www.tcpdump.org/manpages/tcpdump.1.html
