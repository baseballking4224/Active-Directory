<h1>Azure Virtual Machines & Wireshark Network Analysis</h1>

<h1>Project Summary</h1>
This lab shows how I created Windows and Linux virtual machines in Microsoft Azure, configured Network Security Groups (NSGs), and captured various types of network traffic (ICMP, SSH, DHCP, DNS, RDP/TLS) using Wireshark.<br />

<h2>Environments and Technologies Used</h2>

-Azure Portal: Resource Groups, VMs
<p>
-Windows 10 VM (RDP access, Wireshark installed)
  <p>
-Linux (Ubuntu 22.04) VM (SSH connections)

<h2>Technologies </h2>

-NSGs, Virtual Networks
<p>
-Wireshark for traffic capture
 <p> 
-RDP (port 3389), SSH (port 22)
  <p> 
-ICMP, DHCP, DNS, TLS

<h2>High-Level Deployment and Configuration Steps</h2>

Create an Azure Resource Group
<p></p>
I logged into the Azure portal and created a new Resource Group named RG-Network-Activities.
<p></p>
<img width="451" alt="image" src="https://github.com/user-attachments/assets/58fa55a0-5a50-4dc1-af2f-27aeb8691b05" />

<p></p>
<p></p>

Deploy a Windows 10 VM
Next, I deployed a Windows 10 VM in the same region.
-Chose the appropriate size (e.g., Standard B1s)
-Enabled RDP (port 3389) under inbound rules
<img width="461" alt="image" src="https://github.com/user-attachments/assets/79ccc85f-d983-438f-aa57-8dab7298b080" />

<p></p>
<p></p>

Deploy a Linux (Ubuntu) VM
I created a separate Ubuntu 22.04 VM to test cross-platform connectivity:
-Enabled SSH (port 22) under inbound rules
-Chose a lightweight size (e.g., Standard B1s) for cost efficiency
<p></p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/ea950b98-91a6-441d-adaf-0d3993c2fe5a" />


<p>
<p>
Configure Network Security Groups (NSGs)
Under each VM’s Networking blade, I refined inbound rules to allow or block specific traffic:
-Confirmed RDP (3389) for Windows VM
-Confirmed SSH (22) for Linux VM
-Optionally allowed/blocked ICMP by adding a custom rule
<img width="950" alt="image" src="https://github.com/user-attachments/assets/a9055d24-0dd3-400c-a169-a43d2e0dfa1c" />

<p></p>
<p></p>

RDP into Windows VM & Install Wireshark
From my local machine, I used Remote Desktop to log into the Windows VM. Then I downloaded and installed Wireshark. This is crucial for capturing real-time network traffic.
<p></p>
<img width="248" alt="image" src="https://github.com/user-attachments/assets/d1719220-719e-4a80-8bcc-c518e6d19f5e" />
<img width="338" alt="image" src="https://github.com/user-attachments/assets/1cd3bcb7-ace9-4aaf-a584-d27e607fb115" />
  
ICMP (Ping) Traffic Capture
I opened Wireshark on the Windows VM, started a capture on the main network interface, then pinged both the Linux VM and google.com.
<img width="479" alt="image" src="https://github.com/user-attachments/assets/bd81704f-6863-4e75-af52-52dfcdd4e2e7" />

<p></p>
<p></p>

SSH to Linux VM & Analyze Encryption
Next, from the Windows VM’s PowerShell, I ran ssh user@LinuxVM_IP. Wireshark shows encrypted SSH packets on port 22.
<img width="476" alt="image" src="https://github.com/user-attachments/assets/9d22248d-a088-4569-96e8-e0692ce04629" />


<p></p>
<p></p>

DHCP & DNS Analysis
I renewed the IP lease using ipconfig /renew on the Windows VM to see DHCP discover/offer/ack traffic. Then I ran nslookup to capture DNS queries and responses.
<img width="479" alt="image" src="https://github.com/user-attachments/assets/4111687e-bab7-4150-bbb0-d3400496f768" />
<img width="478" alt="image" src="https://github.com/user-attachments/assets/27605255-6388-4eaf-a56b-68bb9fb6cde0" />


<p>
</p>
RDP/TLS Traffic
Finally, I filtered Wireshark by tcp.port == 3389 to examine the encrypted RDP session. This confirmed RDP is encapsulated via TLS for security.
<img width="478" alt="image" src="https://github.com/user-attachments/assets/6d647d81-5bb0-4dbd-b74b-710592638293" />

<p> 
</p>

<H1>CONCLUSION</H1>
By provisioning two Azure VMs (Windows and Linux), tweaking NSG rules, and using Wireshark, I gained practical insight into how different protocols—ICMP, SSH, DHCP, DNS, and RDP—look on the wire. 





