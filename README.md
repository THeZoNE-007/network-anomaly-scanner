Certainly! Below is the `README.md` file tailored to the provided Python script. It includes an overview, features, usage instructions, and other relevant sections.

---

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

## Code Details

### Functions

#### 1. `IP_to_MAC_mapping(packets)`
- Maps IP addresses to their corresponding MAC addresses using the `Ether` layer.
- Returns a dictionary of IP-to-MAC mappings.

#### 2. `Non_Std_ports(packets)`
- Detects traffic on non-standard ports (other than 80, 443, and 22).
- Returns a set of IPs using non-standard ports.

#### 3. `Potential_DDoS_IPs(packets)`
- Identifies IPs with high traffic volume exceeding a threshold (default: 100 packets).
- Returns a list of potential DDoS candidate IPs.

#### 4. `Large_pktSize_IPs(packets)`
- Flags IPs sending packets larger than the standard MTU (1500 bytes).
- Returns a set of IPs with large packet sizes.

#### 5. `ARPreply_unsolicitated(packets)`
- Detects unsolicited ARP replies (ARP replies without prior ARP requests).
- Returns a set of IPs sending unsolicited ARP replies.

#### 6. `Unusual_LargeDNS(packets)`
- Identifies unusually large DNS responses exceeding a size threshold (512 bytes).
- Returns a list of packets with large DNS responses.

#### 7. `ExcessICMP(packets)`
- Detects excessive ICMP Echo Requests within a time window (default: 60 seconds, threshold: 10 requests).
- Returns a list of IPs with excessive ICMP activity.

#### 8. `TCP_SYN_Flood(packets)`
- Detects TCP SYN floods by counting SYN packets exceeding a threshold (default: 100 SYN packets).
- Returns a set of IPs involved in SYN flood attacks.

#### 9. `IPs_scanning_excess_ports(packets)`
- Detects port scanning attempts by identifying IPs connecting to multiple ports (threshold: 5 ports).
- Returns a set of IPs involved in port scanning.

#### 10. `MDP_Calculator(conditions)`
- Calculates the Malicious Detection Percentage (MDP) based on the number of triggered rules.
- Formula: `(satisfied_rules * 100) / 8`.

#### 11. `ReportGen(IPnMAC, C1, C2, C3, C4, C5, C6, C7, C8)`
- Generates a CSV report (`outputReport.csv`) with the following columns:
  - IP Address
  - MAC Address
  - Flags for each detection rule
  - MDP score

---

## Example Output

The generated `outputReport.csv` will look like this:

| IP_Address     | MAC_Address       | Non-Std_Ports | Potential_DDoS | L_Pkt_Size | Unsolicitated_ARP_Replies | Unusually_L_DNS | Excessive_ICMP_Echo_Req | Excessive_TCP_SYN | Excessive_Port_Scanning | MDP(%) |
|----------------|-------------------|---------------|----------------|------------|---------------------------|-----------------|-------------------------|------------------|-------------------------|--------|
| 192.168.1.1    | 00:1A:2B:3C:4D:5E | 1             | 0              | 0          | 1                         | 0               | 0                       | 1                | 0                       | 37.5   |
| 192.168.1.2    | 00:1A:2B:3C:4D:5F | 0             | 1              | 1          | 0                         | 1               | 1                       | 0                | 1                       | 62.5   |

---

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- Built using the [Scapy](https://scapy.net/) library for packet manipulation and analysis.
- Inspired by network security best practices and common threat detection techniques.

---

Feel free to customize this `README.md` further to suit your specific needs or add additional sections such as "Known Issues" or "Future Work." Let me know if you need any further assistance!
