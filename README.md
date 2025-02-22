<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>


# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

This tutorial guides you through the steps to create resources in Azure, observe various types of network traffic using Wireshark, and understand the behavior of different protocols.

## Environments and Technologies Used:
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used:
- Windows 10 (22H2)
- Ubuntu Server 24.04

## Table of Contents
- [Part 1: Create our Resources](#part-1-create-our-resources)
- [Part 2: Observe ICMP Traffic](#part-2-observe-icmp-traffic)
- [Part 3: Observe SSH Traffic](#part-3-observe-ssh-traffic)
- [Part 4: Observe DHCP Traffic](#part-4-observe-dhcp-traffic)
- [Part 5: Observe DNS Traffic](#part-5-observe-dns-traffic)
- [Part 6: Observe RDP Traffic](#part-6-observe-rdp-traffic)

## Part 1: Create our Resources

1. **Create a Resource Group in Azure**

2. **Create a Windows 10 Virtual Machine (VM)**
   - While creating the VM, select the previously created Resource Group.
   - Allow it to create a new Virtual Network (Vnet) and Subnet.

3. **Create a Linux (Ubuntu) VM**
   - Select the previously created Resource Group and Vnet while creating the VM.

4. **Observe Your Virtual Network within Network Watcher**

## Part 2: Observe ICMP Traffic

1. **Use Remote Desktop to connect to your Windows 10 VM**

2. **Within your Windows 10 VM, Install Wireshark**

3. **Open Wireshark and filter for ICMP traffic only**

4. **Retrieve the private IP address of the Ubuntu VM**
   - Attempt to ping it from within the Windows 10 VM.
   - Observe ping requests and replies within Wireshark.

5. **From the Windows 10 VM**
   - Open the command line or PowerShell and attempt to ping a public website (such as www.google.com or www.cisco.com).
   - Observe the traffic in Wireshark.

6. **Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM**

7. **Open the Network Security Group your Ubuntu VM is using**
   - Disable incoming (inbound) ICMP traffic.

8. **Back in the Windows 10 VM**
   - Observe the ICMP traffic in Wireshark and the command line Ping activity.

9. **Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using**

10. **Back in the Windows 10 VM**
    - Observe the ICMP traffic in Wireshark and the command line Ping activity (should start working).
    - Stop the ping activity.

## Part 3: Observe SSH Traffic

1. **Back in Wireshark, filter for SSH traffic only**

2. **From your Windows 10 VM**
   - SSH into your Ubuntu VM (via its private IP address).
   - Type commands (username, pwd, etc.) into the Linux SSH connection and observe SSH traffic in Wireshark.
   - Exit the SSH connection by typing `exit` and pressing [Enter].

## Part 4: Observe DHCP Traffic

1. **Back in Wireshark, filter for DHCP traffic only**

2. **From your Windows 10 VM**
   - Attempt to issue your VM a new IP address from the command line using `ipconfig /renew`.
   - Observe the DHCP traffic appearing in Wireshark.

## Part 5: Observe DNS Traffic

1. **Back in Wireshark, filter for DNS traffic only**

2. **From your Windows 10 VM within a command line**
   - Use `nslookup` to see the IP addresses of google.com and disney.com.
   - Observe the DNS traffic being shown in Wireshark.

## Part 6: Observe RDP Traffic

1. **Back in Wireshark, filter for RDP traffic only (`tcp.port == 3389`)**

2. **Observe the immediate non-stop spam of traffic**
   - **Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?**
     - **Answer**: Because the RDP protocol constantly shows you a live stream from one computer to another, traffic is always being transmitted.

# That's the end of this tutorial.
