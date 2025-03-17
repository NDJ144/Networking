# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

<img width="379" alt="image" src="https://github.com/user-attachments/assets/52eb4271-0fca-4e9e-92ed-f54242ac9260" />

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used

- Windows 10 (21H2)
- Ubuntu Server 20.04

## Overview

This lab demonstrates how to analyze network traffic between Azure VMs and configure Network Security Groups. You'll learn how to:
- Capture and analyze different types of network protocols
- Block specific traffic types using NSGs
- Understand how different network commands generate observable traffic

## Actions and Observations

### Step 1: Create Virtual Machines

1. Create two VMs on Azure:
   - A Linux (Ubuntu Server 20.04) machine
   - A Windows 10 machine
2. Ensure both VMs have two CPUs
3. Ensure both VMs are on the same Virtual Network (VNET)

### Step 2: Install and Configure Wireshark

1. Connect to the Windows VM using Remote Desktop
2. Download and install Wireshark from [https://www.wireshark.org/download.html](https://www.wireshark.org/download.html)
3. Open Wireshark and begin capturing packets

### Step 3: Capture and Analyze ICMP Traffic

1. In Wireshark, set a filter for ICMP traffic only
2. Open Command Prompt and ping the private IP address of your Linux VM
3. Observe the ICMP packets in Wireshark

![image](https://github.com/user-attachments/assets/1c049db5-f840-4ba9-a3eb-c5c2e8a567bf)

4. Inspect an individual packet to see the data being sent in each ping

![image](https://github.com/user-attachments/assets/fdb0b38b-ea28-4bdc-860e-ce7cef19e333)

### Step 4: Configure Network Security Groups to Block ICMP

1. In Command Prompt, use `ping -t [Linux VM's IP]` to continuously ping the Linux VM
2. While the pings are running, go to the Azure Portal
3. Create a new Network Security Group rule on the Linux VM to block inbound ICMP traffic
4. Observe how the ping commands start to time out

![image](https://github.com/user-attachments/assets/a9834110-389f-4a44-b70e-5182b1ef1848)

5. Return to the Azure Portal and modify the NSG rule to allow ICMP traffic again
6. Observe that the ping commands resume receiving replies

![image](https://github.com/user-attachments/assets/3583c5a2-36e4-4021-8d07-c754713a7490)

### Step 5: Capture SSH Traffic

1. In Wireshark, set a filter for SSH traffic only
2. In Command Prompt, use `ssh labuser@[Linux VM's IP]` to connect to the Linux VM
3. Observe the SSH packets being captured in Wireshark

![image](https://github.com/user-attachments/assets/d44f6747-a13e-4dd1-b87e-7c8bb6cf8d40)

### Step 6: Capture DHCP Traffic

1. In Wireshark, set a filter for DHCP traffic
2. In Command Prompt, run `ipconfig /renew` to request a new IP address
3. Observe the DHCP traffic in Wireshark

![image](https://github.com/user-attachments/assets/77be60e5-f3c3-4761-9634-c5001bea8abf)

### Step 7: Capture DNS Traffic

1. In Wireshark, set a filter for DNS traffic
2. In Command Prompt, run `nslookup www.google.com`
3. Observe the DNS query and response in Wireshark

![image](https://github.com/user-attachments/assets/234ee324-c3bd-4181-9009-283f0c343d98)

### Step 8: Observe RDP Traffic

1. In Wireshark, set a filter for RDP traffic using `tcp.port==3389`
2. Notice the constant stream of packets as RDP is continuously sending data between your local computer and the Windows VM

![image](https://github.com/user-attachments/assets/d3ed5cf3-a626-4224-8024-ece4e535a403)

## Conclusion

In this lab, you have:
- Set up Azure VMs for network traffic analysis
- Installed and used Wireshark to capture various network protocols
- Learned how to filter for specific types of traffic (ICMP, SSH, DHCP, DNS, RDP)
- Configured Network Security Groups to control traffic flow
- Observed how different network commands generate specific types of traffic

This practical experience provides a foundation for understanding network protocols, traffic analysis, and security configuration in Azure environments.
