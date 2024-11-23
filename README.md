# Investigating Website Traffic with Wireshark

## Scenario

As a security analyst, I am tasked with examining traffic to a website. I will be analyzing a network packet capture file that contains traffic data related to a user connecting to an internet site. The skill of filtering network traffic using packet sniffers to gather relevant information is crucial in this role.

## Objectives

The objectives of this lab include:
1. **Identify IP Addresses**: Pinpoint the source and destination IP addresses involved in the web browsing session.
2. **Examine Protocols**: Analyze the protocols used when the user connects to the website.
3. **Analyze Data Packets**: Scrutinize data packets to understand the type of information sent and received by the systems during the network data capture.

## Approach

The approach to achieve these objectives involves:
1. **Opening the Packet Capture File**: Begin by opening the packet capture file and exploring the basic Wireshark graphic user interface.
2. **Examining Packet Details**: Dive into a detailed view of a single packet to examine the various protocols and data layers within it.
3. **Applying Filters**: Use filters to select and inspect packets based on specific criteria.
4. **Inspecting UDP DNS Traffic**: Filter and inspect UDP DNS traffic to examine protocol data.
5. **Searching TCP Packet Data**: Apply filters to TCP packet data to search for specific payload text data.

### Task 1: Explore Data with Wireshark

In this task, I will open a network packet capture file that contains data captured from a system that made web requests to a site. My goal is to use Wireshark to get an overview of how the data is presented in the application.

**Steps:**

1. **Open the Packet Capture File:**
   - Double-click the sample packet capture file on the Windows desktop. This action will start Wireshark.
  
2. **Overview of Network Traffic:**
   - Upon opening, a lot of network packet traffic will be listed. Applying filters will help find the necessary information in subsequent steps.

**Key Property Columns for Each Packet:**
- **No.**: Index number of the packet in this capture file.
- **Time**: Timestamp of the packet.
- **Source**: Source IP address.
- **Destination**: Destination IP address.
- **Protocol**: Protocol contained in the packet.
- **Length**: Total length of the packet.
- **Info**: Information about the data in the packet (the payload) as interpreted by Wireshark.

Not all packets are the same color. Coloring rules provide high-level visual cues to quickly classify different types of data. For example, light blue packets contain DNS traffic, while green packets contain a mixture of TCP and HTTP protocol traffic.

![Task_1](URL)


### Task 2: Apply a Basic Wireshark Filter and Inspect a Packet

In this task, I will open a packet in Wireshark for a detailed exploration and filter the data to inspect the network layers and protocols contained within the packet.

**Steps:**

1. **Apply a Display Filter:**
   - Enter the following filter for traffic associated with a specific IP address into the "Apply a display filter..." text box: 
     ```plaintext
     ip.addr == 142.250.1.139
     ```
   - Press `ENTER` or click the Apply display filter icon in the filter text box.
   - The list of packets will be significantly reduced, displaying only packets where either the source or destination IP address matches the entered address. The packets will be color-coded: light pink for ICMP protocol packets and light green for TCP (and HTTP, a subset of TCP) packets.

2. **Inspect a Packet:**
   - Double-click the first packet that lists TCP as the protocol to open a packet details pane window.

3. **Explore the Packet Details Pane:**
   - The upper section contains subtrees with analyses of the various parts of the network packet.
   - The lower section displays the raw packet data in hexadecimal and ASCII text, with placeholder text for non-applicable character data indicated by dots (".").

**Note:** The details pane is located at the bottom portion of the main Wireshark window but can also be accessed in a new window by double-clicking a packet.

4. **Examine Specific Subtrees:**
   - Double-click the first subtree labeled "Frame" to view details about the overall network packet, including frame length and arrival time. Collapse the subtree by double-clicking it again.
   - Double-click the "Ethernet II" subtree to view details about the packet at the Ethernet level, such as source and destination MAC addresses and the type of internal protocol contained within the Ethernet packet. Collapse the subtree.
   - Double-click the "Internet Protocol Version 4" (IPv4) subtree to view packet data about the IP data contained in the Ethernet packet, including source and destination IP addresses and the internal protocol (TCP or UDP). The source and destination IP addresses here match those in the summary display of this packet in the main Wireshark window. Collapse the subtree.
   - Double-click the "Transmission Control Protocol" (TCP) subtree to view detailed information about the TCP packet, such as source and destination TCP ports, TCP sequence numbers, and TCP flags. The source and destination ports listed here match those in the info column of the summary display for this packet in the list of all packets in the main Wireshark window.

**TCP Destination Port:**
   - The TCP destination port of this TCP packet is port 80.
   
5. **Inspect TCP Flags:**
   - In the Transmission Control Protocol subtree, scroll down and double-click "Flags" to view detailed information about the TCP flags set in this packet.

6. **Close the Detailed Inspection Window:**
   - Click the X icon to close the detailed packet inspection window.

7. **Clear the Display Filter:**
   - Click the X Clear display filter icon in the Wireshark filter bar to clear the IP address filter.

By completing this task, I will have a comprehensive understanding of how to apply filters in Wireshark and inspect the detailed layers and protocols of network packets.

![Task_2](URL)

### Task 3: Use Filters to Select Packets

In this task, I will use filters to analyze specific network packets based on their source or destination. This involves selecting packets using either their physical Ethernet Media Access Control (MAC) address or their Internet Protocol (IP) address.

**Steps:**

1. **Filter Traffic for a Specific Source IP Address:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     ip.src == 142.250.1.139
     ```
   - Press `ENTER` or click the Apply display filter icon.
   - A filtered list will be displayed with fewer entries, showing only packets from the IP address 142.250.1.139.

![Task_2](URL)

2. **Clear the IP Address Filter:**
   - Click the X Clear display filter icon in the Wireshark filter bar.

![Task_2](URL)

3. **Filter Traffic for a Specific Destination IP Address:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     ip.dst == 142.250.1.139
     ```
   - Press `ENTER` or click the Apply display filter icon.
   - A filtered list will be displayed with only packets sent to the IP address 142.250.1.139.

4. **Clear the IP Address Filter:**
   - Click the X Clear display filter icon in the Wireshark filter bar.

5. **Filter Traffic for a Specific Ethernet MAC Address:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     eth.addr == 42:01:ac:15:e0:02
     ```
   - Press `ENTER` or click the Apply display filter icon.
   - Double-click the first packet in the list (you may need to scroll back to display the first packet in the filtered list).

6. **Inspect Ethernet II and IP Subtrees:**
   - Open the "Ethernet II" subtree to verify the MAC address is listed as either the source or destination address.
   - Collapse the "Ethernet II" subtree and expand the "Internet Protocol Version 4" subtree to view details such as the Time to Live and Protocol fields.

**Question:**
   - What is the protocol contained in the Internet Protocol Version 4 subtree from the first packet related to MAC address 42:01:ac:15:e0:02?
     - TCP
![Task-_3](URL)


### Task 4: Use Filters to Explore DNS Packets

In this task, I will use filters to select and examine DNS traffic, exploring how DNS packet data contains both queries and answers.

**Steps:**

1. **Filter for UDP Port 53 Traffic:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     udp.port == 53
     ```
   - Press `ENTER` or click the Apply display filter icon.
   - Double-click the first packet in the list to open the detailed packet window.

2. **Inspect DNS Query:**
   - Expand the "Domain Name System (query)" subtree and then expand "Queries" to find the queried website name (opensource.google.com).

![Task_4](URL)

3. **Inspect DNS Answer:**
   - Open the fourth packet in the list, expand "Domain Name System (query)" and then "Answers" to view the IP addresses associated with the queried name.

![Task_4](URL)

### Task 5: Use Filters to Explore TCP Packets

In this task, I will use additional filters to select and examine TCP packets, learning to search for text in payload data.

**Steps:**

1. **Filter for TCP Port 80 Traffic:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     tcp.port == 80
     ```
   - Press `ENTER` or click the Apply display filter icon.
   - Double-click the first packet in the list to inspect the details.

**Questions:**
   - What is the Time to Live value of the packet in the Internet Protocol Version 4 subtree?
     - 64
    
![Task_5](URL)
   
   - What is the Frame Length of the packet in the Frame subtree?
     - 54 bytes

![Task_5](URL)     
   
   - What is the Header Length of the packet in the Internet Protocol Version 4 subtree?
     - 20 bytes

![Task_5](URL)     
   
   - What is the Destination Address in the Internet Protocol Version 4 subtree?
     - 169.254.169.254

![Task_5](URL)

2. **Close the Inspection Window and Clear the Filter:**
   - Click the X icon to close the detailed packet inspection window.
   - Click the X Clear display filter icon to clear the filter.

3. **Filter for Specific Text in TCP Packets:**
   - Enter the following filter into the "Apply a display filter..." text box:
     ```plaintext
     tcp contains "curl"
     ```
   - Press `ENTER` or click the Apply display filter icon to filter packets containing web requests made with the curl command.

![Task_5](URL)

## Conclusion

In this exercise, I demonstrated practical experience using Wireshark to:
- Open saved packet capture files.
- View high-level packet data.
- Use filters to inspect detailed packet data.

I applied essential skills in filtering and analyzing network traffic, identifying IP addresses, examining protocols, and scrutinizing data packets. These skills are critical for a security analyst to investigate and secure network communications effectively. This is an important milestone in understanding how to use network packet analysis tools to examine network traffic.

