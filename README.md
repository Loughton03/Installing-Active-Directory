<p align="center">
<img src="https://i.imgur.com/ouRvZVR.png" alt="place-holder"/>
</p>

<h1>Installing Active Directory </h1>
In this lab, I explored and analyzed network traffic to and from Azure virtual machines using Wireshark and experimented with network security groups to better understand their impact on traffic control.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop Connection
- Active Directory Domain Services

<h2>Operating Systems Used</h2>

- Windows 10 Pro
- Windows Server 2022

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/y95slsb.png" height="80%" width="80%" alt="static-IP"/>
</p>

<p>
First, I set the IP address of the domain controller VM to static. By default, Azure VMs use dynamic IPs, which can disrupt connectivity between VMs, even within the same vNet. Setting a static IP ensures consistent network access for the domain. In the Azure portal, I navigated to the Networking tab on the domain controller VM, selected its Network Interface, and opened the IP configurations tab. I then changed the IP Assignment setting to Static and saved the changes. This static IP will be referenced in future configurations.
</p>

<p>
<img src="https://i.imgur.com/yP2eUSp.png" height="80%" width="80%" alt="Ping dc-1"/>
</p>

<p>
<img src="https://i.imgur.com/CLkbNLf.png" height="80%" width="80%" alt="place-holder"/>
</p>

<p>
<img src="https://i.imgur.com/iPiaLZ4.png" height="80%" width="80%" alt="place-holder"/>
</p>

<p>
To confirm connectivity, I logged into the client VM and used the command ping -t [domain controller private IP address]. Initially, the ping timed out. This was due to ICMPv4 being disabled in Windows Firewall on the domain controller VM. I enabled it by opening Windows Defender Firewall (using wf.msc), navigating to Inbound Rules, and enabling the "Core Networking Diagnostics - ICMP Echo Request" rule. Returning to the client VM, I confirmed successful ping responses, indicating connectivity.
</p>

<img src="https://i.imgur.com/poEIoQ5.png" height="80%" width="80%" alt="place-holder"/>

<p>
With connectivity confirmed, I installed Active Directory Domain Services on the domain controller VM. Using Server Manager, I selected "Add Roles and Features," confirmed the private IP of the domain controller, selected the Active Directory Domain Services role, and completed the setup. Afterward, I promoted the server to a domain controller by clicking the notification flag in Server Manager and selecting "Promote this server to a domain controller." I created a new forest with the domain name "ernestotest.com" and set a password. Following the prompts, I completed the installation.  
</p>


<p>
<h3>Important Note</h3>
When reconnecting to the domain controller VM through Remote Desktop, it's essential to log in using the domain context. The username should include the domain path, e.g., PLEASE CHANGE.com\labuser. With Active Directory installed, future labs will build on this setup, allowing the client VM to join the established domain for further configuration and exploration.
</p>
