# 💻 tcpdump

## 🎯 Purpose

tcpdump is a powerful, CLI-based network packet analyzer used to capture, inspect, and filter network traffic directly from the terminal. It is essential for troubleshooting network issues, performing lightweight remote monitoring, and creating packet captures for later forensic analysis.

## 🧠 Key Concepts

* **Network Interfaces:** Physical or virtual network adapters (e.g., `eth0`, `wlan0`, `any`) listened to for traffic.

* **Berkeley Packet Filter (BPF):** A flexible syntax used to filter incoming network packets before they are processed or written to disk.

* **Packet Capturing & Reading:** Capturing live interface traffic directly to memory or saving it to standard `.pcap` files for offline analysis.

* **DNS Resolution Control:** Controlling whether IP addresses and ports are automatically converted into hostnames and service names.

## 💻 Commands

```bash
# List available network interfaces
sudo tcpdump -D

# Capture traffic on a specific interface
sudo tcpdump -i eth0

# Capture without resolving hostnames or port names (faster & cleaner)
sudo tcpdump -n -nn -i eth0

# Limit the capture to a specific number of packets
sudo tcpdump -c 20 -i eth0

# Save captured packets to a PCAP file
sudo tcpdump -w capture.pcap -i eth0

# Read and display packets from a PCAP file
sudo tcpdump -r capture.pcap
```

## 📋 Examples

* **Filter by Host or Subnet:**
  ```bash
  sudo tcpdump -i eth0 host 192.168.1.10
  sudo tcpdump -i eth0 net 10.0.0.0/24
  ```

* **Filter by Port or Protocol:**
  ```bash
  sudo tcpdump -i eth0 port 80
  sudo tcpdump -i eth0 icmp
  ```

* **Combine BPF Logic Filters:**
  ```bash
  sudo tcpdump -i eth0 "src host 192.168.1.50 and (port 80 or port 443)"
  ```

## 🔎 Investigation

* **Display ASCII Data Payload:** Use `-A` to print packet content in ASCII (useful for inspect HTTP headers or plaintext strings).
  ```bash
  sudo tcpdump -A -i eth0 port 80
  ```

* **Display Hexadecimal and ASCII Data:** Use `-XX` to inspect raw binary data along with hex offset values.
  ```bash
  sudo tcpdump -XX -i eth0 icmp
  ```

* **Identify Suspicious Port Activity:** Filter for non-standard ports or sudden high-volume connections from an isolated host IP.

## ⚠️ Important

* **Privileges Required:** Capturing traffic on raw network sockets requires root or `sudo` privileges.

* **Buffer Overflows:** High-traffic networks can drop packets if tcpdump is forced to output too much detailed text to the terminal screen.

## 🛡️ Security

* Protect generated `.pcap` files with restricted permissions (`chmod 600`), as they may contain sensitive cleartext data (credentials, session cookies, API keys).

* Avoid capturing unneeded payload data on production networks to prevent unintended data exposure.

## 📚 References

* [tcpdump Official Man Page](https://www.tcpdump.org/manpages/tcpdump.1.html)

* [Sans Security tcpdump Cheat Sheet](https://www.sans.org/posters/tcpdump-cheat-sheet/)