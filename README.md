<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



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
  To begin observing the network traffic, Click on the blue shark fin icon. This will show all the information that is going in and out of the virtual machine. There is quite a lot of information. To make use of this information it is important to use filters. The first filter we will explore will focus on ICMP, or Ping. Type ICMP into the filter bar at the top of the window, to filter out all information that is not ICMP traffic. Notice that there is not any Ping data at this time. 

  Minimize the WIndows Virtual Machine, and bring up Azure. Locate and copy the private IP address for the Linux machine you made earlier. We will use this to test Ping connectivity, or ICMP traffic. Once you have copied, or otherwise noted the IP address, return to the Windows Virtual Machine. 
  </p>
  <p>
<img src="https://i.imgur.com/99RElOd.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Using the search function of the Start Menu, locate "PowerShell", and open the program. Type into the command line "ping (Linux Machine's Private IP Address)". As seen in the above picture. Press "enter". This will trigger a reaction in both PowerShell, and in Wireshark, as the ICMP data is sent and received. Observe the call and response of the Ping of ICMP data between the two machines. This can be seen not just between the two machines set up in this activity, but also between any two machines. Try pinging "Google.com", and observe the same call and response that you saw between the two control machines.

  The next step of our activity will involve Azure network Security Groups. While PowerShell is still open, type "ping (Linux Machine's Private IP Address) -t" to create a perpetual ping. You should see a continuous flow of data with each call and response between the two machines. Minimize the Windows Virtual Machine, and bring up the Azure portal. Using the Search bar, look for "Network Security Groups''. Open the page, and select the Linux machine in the list of network security groups provided. Navigate to "Inbound Security Rules'' on the left-hand menu, and click on it to open the page. Notice the rules listed for incoming data traffic. To create a new rule, click the "+ Add'' button. 

  For the purposes of this activity, select the following options for this new rule
  Source: any
  Source Port Ranges: Any
  Destination: Any
  Protocol: ICMP
  Action: Deny
  Priority: 200
  Name: DENY_ICMP

  Finalize the rule, by clicking "Add". This will install the new rule that will stop all ICMP traffic. Bring up the Windows Virtual Machine. Observe that the flow of Data in Wireshark no longer has replies from the Linux machine now that the rule is in place. Minimize the Microsoft Windows Virtual Machine, and bring up the Azure portal. Click on the rule name to edit the rule we just created. Change the Action from "Deny", to "Allow", and save the changes. Bring up the Windows Virtual Machine again, and observe how the Requests from the continuous ping are once again receiving replies. 

  End the continuous ping by pressing "Ctrl+C"
</p>
<br />

<h2>Observe SSH Traffic</h2>
<p>
<img src="https://i.imgur.com/uAj8K1A.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/mDYjw3N.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Wireshark, change the filter from "ICMP" to "SSH". Refresh the list to clear the previous activity, and to start with a cleared screen. In PowerShell, type the command "ssh (UserID)@(Linux Machine's Private IP Address)", as seen in the image above. Hit enter, and observe the data as it appears in Wireshark. Type "Yes", and enter the password you created for the Linux machine. Note that the password will not appear as you type it in SSH. This is normal. You should now have an open connection to the Linux machine through SSH. PowerShell is now connected to the Linux Command line, so Linux Commands will have the intended effect. Notice the data travel across the network with each command that is entered. To close the SSH Session, Type "exit". Once the session is closed, notice that commands in PowerShell no longer generate new SSH data.
</p>
<br />

<h2>Observe DHCP Traffic</h2>
<p>
<img src="https://i.imgur.com/L5OpLdm.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
  In Wireshark, Change the filter to "DHCP", and refresh. As this dataset is used for IP address configuration, the easiest way to observe this data transfer is to type "ipconfig /renew", in PowerShell. THer is a chance that the Remote Desktop session could disconnect for a moment as Azure handles the request for a new IP address, but it should reconnect. Observe the DHCP traffic from the request, in Wireshark.
</p>
<br />

<h2>Observe DNS Traffic</h2>
<p>
<img src="https://i.imgur.com/akZn0qj.jpeg" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Change the filter, in Wireshark, to look for DNS traffic. it is possible that ther will already be entries when you switch to this filter. Go ahead and clear this data, and start with a clear screen. DNS traffic will happen in the background. clearing it only makes it easier to see the data that is entered as part of this activity. in PowerShell, type "nslookup www.google.com" top instruct the machine to gather data about the DNS of "Google.com". Observe the data exchange on Wireshark, as this request is fulfilled. 
</p>
<br />

<h2>Observe RDP Traffic</h2>
<p>
 Change the Filter in Wireshark to RDP. Since we are using Remote Desktop into a Virtual Machine, there is RDP traffic flowing constantly over the network. Observe the data flow continuously due to the active session. As long as the session remains active, this datastream will not stop. Whatever is done on the host computer is transmitted to the Virtual Machine, and both machines are synced repeatedly.
</p>
<br />

<h2>Clean Up</h2>
<p>
This concludes the activity tutorial. Make sure all resources in Azure are deleted before ending your computer session for the day. Remember, all instances cost money over time. It is important to delete any machine, or instance you are no longer using. 
</p>
