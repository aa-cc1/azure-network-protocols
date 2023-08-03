<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Observe ICMP traffic and disable inbound requests
- Observe SSH, DHCP, DNS, and RDP traffic in Wireshark
- Utilize CLI commands such as ping, nslookup, and ipconfig /renew

<h2>Actions and Observations</h2>

_⚠️Before we start, if you haven't already, go ahead and create a **Microsoft Azure** account with an active subscription._
#

xxx1  We are going to create ***two*** VMs inside a RG(resource group); one will be running Windows 10 (vm1) and the other Ubuntu Linux(vm2). (use Netowrk Watcher via topology to confirm that they are both on the same network) 
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Locate the ***Public IP*** address for VM1 as we will use this to remote in using Windows Remote Desktop. Within the Virtual Machine we will install Wireshark (select the version for your OS).
<img src="Screenshot (145).png"/>
</p>
<br />

xxx3 Retrieve the ***Private IP*** address for VM2 (Ubuntu Linux). 
<img src="Screenshot (150).png"/>

Within the Virtual Machine, open ***Wiereshark and Powershell***. We will ping VM2 in Powershell (or Command Line) and filter for ICMP traffic in Wireshark. Try pinging a _www.google.com_ or any website and observe the traffic. 

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
xxx4 Iniate a _perpetual_ ping to VM2 (Ubuntu Linux). It should look something like this ***ping -t 10.x.x.x -4*** . We're going to open the ***Nework Security Group*** in Azure for VM2 (Ubuntu Linux) and _disable_ icoming ICMP traffic. Go back to the Virtual Machine and observe the traffic in Wireshark and Powershell/Command Line. It should be timing out. Re-enable the ICMP traffic and observe the change, then stop the ping activity.

</p>
<br />
In Wireshark filter for SSH traffic. We are going to use SSH into the VM2 (Ubuntu Linux). Back in Wireshark filter for DHCP. We are going to request a new IP address by running _ipconfig /renew_  and observe the DHCP traffic.

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Filter for DNS traffic in Wireshark. From the command line use nslookup to find the IP addresses for google.com and disney.com (you can also try this with any public website). Observe the traffic in Wireshark.
Filter for RDP traffic in Wireshark. Observe the traffic. Notice anything different? Its constantly updating because we have an active session from one computer to another.
  
</p>
<br />
