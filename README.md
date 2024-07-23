<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Clean Up

<h2>Create Resources</h2>
<p>
To get started with this exploration of Network communication, we will need to set up two virtual Machines in Azure. For the sake of clarification, one virtual machine will be running Windows 10, and the other will run Linux. When creating these Virtual Machines, make sure they share the same Virtual network, and Subnet. This will allow the two virtual Machines to interact with each other.
</p>
<br />

<h2>Observe ICMP Traffic</h2>
<p>
<img src="https://i.imgur.com/odPggfQ.png" height="40%" width="40%" alt="Wireshark"/>
</p>
<p>
  Using Microsoft Remote Desktop, Log into the windows Virtual Machine. To view the data traffic, we will use a program known as WireShark. To install Wireshark in the Windows Virtual Machine, Open up Microsoft Edge, and Google search "Download Wireshark", or go to "https://www.wireshark.org/download.html". Download and run the Installation file. For the purposes of this tutorial, a default installation will suffice. Allow the installation Wizard to complete the process. Close Microsoft Edge, and open Wireshark. 
</p>
  <p>
<img src="https://i.imgur.com/TDsBy9c.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
  To begin the observing network traffic, Click on the blue sharkfin icon. This will show all the information that is going in and out of the virtual machine. Ther is quite a lot of information. To make use of this information it is important to use filters. The first filter we will explore will focus on ICMP, or Ping. Type ICMP into the filter bar at the top of the window, to filter out all information that is not ICMP traffic. Notice that there is not any Ping data at this time. 

  Minimize the WIndows Virtual Machine, and bring up Azure. Locate and copy the private IP address for the Linux machine you made earlier. We will use this to test Ping connectivivity, or ICMP traffic. Once you have copied, or otherwise noted the IP address, return to the Windows Virtual Machine. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
