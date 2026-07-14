<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This project demonstrates the deployment of Windows and Linux virtual machines in Microsoft Azure to analyze network traffic using Wireshark. Common network protocols, including ICMP, SSH, DHCP, DNS, and RDP, are examined while Azure Network Security Groups (NSGs) are configured to observe how firewall rules affect network communication. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2) for main
- Ubuntu Server 20.04 for secondary

<h2>Prerequisites</h2>

- Windows Virtual Machine up and running
- Ubuntu Virtual Machine up and running
- Both Virtual Machines are on the same Virtual Network / Subnet

<h2>High-Level Steps</h2>

1 - Create our Virtual Machines

2 - Observe ICMP Traffic

3 - Configuring a Firewall [Network Security Group]

4 - Observe Traffic (DHCP, DNS, RDP)

<h2>Actions and Observations</h2>

Within the Windows VM, install WireShark
<p>
<img width="1664" height="553" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/3a3298fb-ab8e-44e1-804b-64e26b91f271" />

</p>
<p>
</p>
<br />
In Wireshark, filter for ICMP traffic ONLY
<p>
<img width="636" height="327" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/a4d10126-cc3f-4d19-89b6-a0b6d9b09d50" />
</p>
<p>
</p>
<br />
Attempt to ping the Ubuntu VM from the Windows VM
<p>
<img width="534" height="172" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/63cec3ee-630b-4057-ae57-3121cf781d93" />
</p>
- Observe ping requests and replies within WireShark
<p>
</p>
<br />
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
<p>
<img width="387" height="559" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/c54da0b2-7d3d-4f39-b33c-cb9f847f5e40" />
</p>
<p>
</p>
<br />
Observe the ICMP traffic in WireShark and the command-line Ping activity (for non-stop ping, use "ping *IP* -t")
<p>
<img width="1074" height="510" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/5faa6f39-d86d-4c85-ad1a-4dcc313cb6e3" />
Now re-enable ICMP traffic for the Network Security Group on your Ubuntu VM

- Observe the ICMP traffic on the Windows VM as it starts back up 
- Stop the ping
</p>

<p>

<br />
Now filter for SSH traffic ONLY
<p>
<img width="567" height="292" alt="Screenshot (7)" src="https://github.com/user-attachments/assets/a30efd05-e5a7-4eef-af48-846bff8d970a" />
</p>

<br />


Windows 10 VM, “SSH into” your Ubuntu Virtual Machine using its private IP address
<p>
<img width="1540" height="868" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/df1fa195-8eb4-4d6f-902e-da95bb5411e6" />
</p>
<p>
-Enter the password for the Ubuntu machine to log in
</p>
<br />



Once you have "SSHed into" the Ubuntu VM, enter commands and observe traffic on WireShark
<p>
<img width="1071" height="649" alt="Screenshot (10)" src="https://github.com/user-attachments/assets/c6aed440-3950-4274-b242-be4ea45d433a" />
</p>
<p>
-Type "exit" to log out of the Ubuntu machine 
</p>
<br />


In Wireshark, inside the Windows VM, filter for DHCP traffic only
<p>
<img width="523" height="226" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/e95ba321-e658-4d00-abc0-3ac24dfaafcf" />
</p>
<p>
Open PowerShell as admin and run: ipconfig /renew
</p>

<p>
<img width="1071" height="343" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/8a8429ea-89a1-4820-8728-fa872f861bba" />

</p>
<p>
- Observe the DHCP traffic appearing in WireShark
</p>

<br />

Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
<p>
<img width="936" height="643" alt="Screenshot (20)" src="https://github.com/user-attachments/assets/66cab2c3-468f-4479-9c1c-05132226c0c8" />
</p>
<p>
Observe the immediate non-stop spam of traffic
  - RDP is constantly showing you a live stream from one computer to another, so the traffic is always being transmitted
</p>
<br />

In Wireshark, filter for DNS traffic only
<p>
<img width="609" height="516" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/eb74955e-815b-46b0-8102-cc2816f68bf1" />
</p>
<p>
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
<p> 
- Observe the DNS traffic being shown in WireShark
