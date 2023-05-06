<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this demonstration, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Use Azure VMs and Remote Desktop to Begin
- Download/Install Wireshark
- Observe Network Traffic
- Add an Inbound Security Rule and Observe the Effects
- Test Various Network Protocols


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/pqxfPdI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After configuring the resource group and virtual machines, and connecting to one of the virtual machines with the remote desktop application, the hostname and username can be observed. The username was previously randomly generated with Powershell. 
</p>
<br />

<p>
<img src="https://i.imgur.com/F4fAQkn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To download Wireshark, wireshark.org/download/html should be accessed, and "Windows Installer (64-bit)" should be selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/yYCsZZf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The installation of Wireshark on the virtual machine has been successfully completed.
</p>
<br />

<p>
<img src="https://i.imgur.com/jXiTFdJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After opening Wireshark, the ethernet adaptor should be selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/wy5ClNj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
It can be seen that there is not any network traffic; this is because ICMP was entered into the top left corner. ICMP is the protocol that ping uses; ping is used to test connectivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/ldeERZf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After opening Powershell_ise, a perpetual ping is entered; network traffic can now be seen in Wireshark. The private address for the second virtual machine that was created was needed for the perpetual ping command (ping -t 10.0.0.4). The successful replies and requests can be observed, as well as the sources and destinations between the two virtual machines.
</p>
<br />

<p>
<img src="https://i.imgur.com/YB8yF7M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The perpetual ping is terminated with the Control-C command.
</p>
<br />

<p>
<img src="https://i.imgur.com/cgL7Ojp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within Azure VMs, the network security group for the virtual machine is accessed. The goal here is to deny inbound ICMP traffic. "Inbound security rules" is selected, and then "Add inbound security rule". The security rule is configured to deny IMCP traffic, and is set with a priority (200) that is less than the next highest priority (300); this ensures thatthe added rule holds the highest priority.
</p>
<br />

<p>
<img src="https://i.imgur.com/3haDQBr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
It can be seen that the perpetual ping has begun to time out; the firewall and security rule are in effect.
</p>
<br />

<p>
<img src="https://i.imgur.com/UpMhkt8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
If the security rule was instead set to "Allow" rather than "Deny"... 
</p>
<br />

<p>
<img src="https://i.imgur.com/hiXtioN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
...the connectivity is again established, since the ICMP has been opened up on the virtual machine's firewall. 
</p>
<br />

<p>
<img src="https://i.imgur.com/9zxWZnV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DCHP traffic will now be observed; DHCP is used to automatically assign IP addresses.
</p>
<br />

<p>
<img src="https://i.imgur.com/0yOXksQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To force a renewal of an IP adress, the command "ipconfig /renew" can be entered. It can be seen that the DHCP traffic was solely one request and one reply, reissuing the IP address. 
</p>
<br />

<p>
<img src="https://i.imgur.com/gCAiTM9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DNS traffic will now be observed. Within the Powershell command line, "nslookup www.google.com" is entered. This command, essentially, is asking the DNS, google.com, what it's IP address(es) are.
</p>
<br />

<p>
<img src="https://i.imgur.com/UdgJYnP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
TCP port 3389 traffic (remote desktop protocol) will now be observed. Despite not enterign a command on Powershell, it can be seen that there is still ample traffic. This is because there is a live/active RDP session from the host computer to the virtual machine that is currently being used.
</p>
<br />

