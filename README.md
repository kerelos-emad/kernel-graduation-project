# kernel-graduation-project

## Network Task Requirements Document


### 1. Objective
The primary objective of this network task is to analyze network traffic using Wireshark and automate specific tasks with a Bash script, generating a summary report.


### 2. Scope
1. Capture network traffic using Wireshark.
2. Develop a Bash script to analyze the captured data.
3. Extract relevant information like total packets, protocols, and top source/destination IP addresses.
4. Generate a summary report based on the analysis.


### 3. Prerequisites
1. Wireshark installed.
2. Permission to capture network traffic.
3. Basic Bash scripting knowledge.


### 4. Wireshark Capture
1. Start Wireshark and capture network traffic.
2. Save the captured data in a pcap file (e.g., your_capture_file.pcap).



## 5. Bash Script
1. Create a Bash script named analyze_traffic.sh.
* Use the script to:
a. Specify the path to the Wireshark pcap file.
b. Analyze the data to identify patterns.
c. Extract information like total packets, protocols, etc.
d. Generate a summary report.



### Hints:

1. Research Wireshark command-line tools like tshark for packet analysis.
2. Use filters to focus on HTTP (http) and HTTPS/TLS (tls) protocols.
3. Explore options for counting packets, extracting IP addresses, and generating summary statistics.

### 6. Output
The Bash script should output a summary report containing identified patterns and key statistics.




### 🏁🏁🏁🏁 Bash script startup code.


```bash
#!/bin/bash

# Bash Script to Analyze Network Traffic

# Input: Path to the Wireshark pcap file
pcap_file="$1"
tshark_path="/path/to/tshark"  # Update this with the actual path to tshark

# Function to extract information from the pcap file
analyze_traffic() {
    # Use tshark with the specified path for packet analysis.
    total_packets=$("$tshark_path" -r "$pcap_file" | wc -l)
    http_packets=$("$tshark_path" -r "$pcap_file" -Y "http" | wc -l)
    https_packets=$("$tshark_path" -r "$pcap_file" -Y "tls" | wc -l)
    top_source_ips=$("$tshark_path" -r "$pcap_file" -T fields -e ip.src | sort | uniq -c | sort -nr | head -n 5)
    top_dest_ips=$("$tshark_path" -r "$pcap_file" -T fields -e ip.dst | sort | uniq -c | sort -nr | head -n 5)

    # Output analysis summary
    echo "----- Network Traffic Analysis Report -----"
    echo "1. Total Packets: $total_packets"
    echo "2. Protocols:"
    echo "   - HTTP: $http_packets packets"
    echo "   - HTTPS/TLS: $https_packets packets"
    echo ""
    echo "3. Top 5 Source IP Addresses:"
    echo "$top_source_ips"
    echo ""
    echo "4. Top 5 Destination IP Addresses:"
    echo "$top_dest_ips"
    echo ""
    echo "----- End of Report -----"
}

# Check if the pcap file argument is provided
if [ -z "$pcap_file" ]; then
    echo "Usage: ./analyze_traffic.sh /path/to/your_capture_file.pcap"
    exit 1
fi

# Run the analysis function
analyze_traffic


```










----------------------------------

#### 🗒️ 🗒️ 🗒️ 🗒️ Expected Input:

Suppose you have a Wireshark pcap file named network_traffic.pcap containing a mix of HTTP and HTTPS traffic.




#### 🗒️ 🗒️ 🗒️ 🗒️Expected Output:

```txt
----- Network Traffic Analysis Report -----
1. Total Packets: 1000
2. Protocols:
   - HTTP: 600 packets
   - HTTPS/TLS: 400 packets

3. Top 5 Source IP Addresses:
   - 192.168.1.1: 300 packets
   - 192.168.1.2: 200 packets
   - ...

4. Top 5 Destination IP Addresses:
   - 10.0.0.1: 400 packets
   - 10.0.0.2: 300 packets
   - ...

----- End of Report -----


```







### Please Submit task to receive your first 🧑‍🎓🧑‍🎓🧑‍🎓🧑‍🎓🧑‍🎓
