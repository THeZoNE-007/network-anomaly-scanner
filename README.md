# Network Traffic Analysis Tool

## Overview

This Python script analyzes network traffic from a PCAP file to detect suspicious activities using multiple detection rules. It generates a report in CSV format, summarizing the findings and assigning a **Malicious Detection Percentage (MDP)** score to each IP address.

The tool leverages the `scapy` library for packet parsing and analysis.

---

## Features

### Detection Rules
1. **Non-Standard Ports**: Identifies traffic on ports other than standard ones (e.g., 80, 443, 22).
2. **High Traffic Volume**: Detects potential DDoS activity by counting packets exceeding a threshold.
3. **Large Packet Sizes**: Flags IPs sending packets larger than the standard MTU (1500 bytes).
4. **Unsolicited ARP Replies**: Identifies ARP replies without corresponding ARP requests.
5. **Unusually Large DNS Responses**: Detects DNS responses exceeding a size threshold (512 bytes).
6. **Excessive ICMP Requests**: Flags IPs sending too many ICMP Echo Requests within a time window.
7. **TCP SYN Flood**: Identifies potential SYN flood attacks based on SYN packet counts.
8. **Port Scanning**: Detects IPs attempting connections to multiple ports.

### Output
- A CSV file (`outputReport.csv`) is generated with the following columns:
  - IP Address
  - MAC Address
  - Flags for each detection rule (1 = triggered, 0 = not triggered)
  - Malicious Detection Percentage (MDP) score

---

## Requirements

### Prerequisites
- Python 3.x
- Required Python libraries:
  - `scapy`
  - `collections`
  - `csv`

### Installation
1. Install the required dependencies:
   ```bash
   pip install scapy
   ```

2. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/network-traffic-analysis.git
   cd network-traffic-analysis
   ```

---

## Usage

### Running the Script
1. Place your PCAP file in the same directory as the script or provide its path.
2. Run the script using the following command:
   ```bash
   python script_name.py <path_to_pcap_file>
   ```
   Example:
   ```bash
   python script_name.py example_traffic.pcap
   ```

3. The script will generate a CSV file named `outputReport.csv` in the same directory.

---

---

## Example Output

The generated `outputReport.csv` will look like this:

| IP_Address     | MAC_Address       | Non-Std_Ports | Potential_DDoS | L_Pkt_Size | Unsolicitated_ARP_Replies | Unusually_L_DNS | Excessive_ICMP_Echo_Req | Excessive_TCP_SYN | Excessive_Port_Scanning | MDP(%) |
|----------------|-------------------|---------------|----------------|------------|---------------------------|-----------------|-------------------------|------------------|-------------------------|--------|
| 192.168.1.1    | 00:1A:2B:3C:4D:5E | 1             | 0              | 0          | 1                         | 0               | 0                       | 1                | 0                       | 37.5   |
| 192.168.1.2    | 00:1A:2B:3C:4D:5F | 0             | 1              | 1          | 0                         | 1               | 1                       | 0                | 1                       | 62.5   |

---

## Acknowledgments

- Built using the [Scapy](https://scapy.net/) library for packet manipulation and analysis.
- Inspired by network security best practices and common threat detection techniques.
