<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group
- Create a Virtual Machine
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
<h2>Actions and Observations</h2>
<br />
<br />
<h3 align="center;">
  Set up your virtual environment
</h3>
<br />
<p>To begin,we'll set up a Resource Group within azure,I typically create the VM in (US) West US 2.</p>

<p>
<img src="https://i.imgur.com/3ysjv2n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>When setting up the VM,choose th Resource Group you created earlier and allow it to generate</p>
<p>a new virtual Network{Vnet} and subnet. Ensure you select the password option in the <mark>Administrator Account section.</mark></p>
<p>
<img src="https://i.imgur.com/EhgAENq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Create an ubuntu virtual machine</p>
<p>During the VM creation process,select the resource group you created earlier and enable the cxreation of a</p>
<p>new Virtual Network {Vnet} and subnet.Ensure that the password option is chosen in the <mark>Administrator Account section</mark></p>
<p>{not visible in the image}</p>
<p>
<img src="https://i.imgur.com/ETVecdH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>Observe Your Virtual Network within Network Watcher.</p>
 <p>
   <img src="https://i.imgur.com/8dtqJPo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 </p>
<br />
<br />
<p><h3 align="center;">
  Now let's observe some ICMP traffic
</h3></p>
<br />
<p>Connect to your Windows 10 VM,install wireshark,launch the aplication,and set the filter to display only ICMP traffic.</p>
<img src="https://i.imgur.com/PkWQw8k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>Find the private IP adress of the Ubuntu VM and try pingin it from the windows 10VM.</p>
<p>Use wire shark to monitor and observe the ping requests and replies.</p>
<img src="https://i.imgur.com/OQc70EW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/k9NazjE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>Try to ping a public website {such as www.google.com} and watch the traffic in wireshark:</p>
<img src="https://i.imgur.com/Jg7G3aS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>Initiate a perpetual/nono-stop ping from your windows 10 VM to your ubuntu VM:</p>
<img src="https://i.imgur.com/s9BcFUH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>Access the Network Security Group{NSG} associated with your ubuntu VM and block inbound ICMP traffic.</p>
<p>Then,switch back to the windows 10 VM to monitor the ICMP traffic in wireshark and observe the ping</p>
<p>command results in the terminal.</p>
<img src="https://i.imgur.com/0EVKLeb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/76tYZ52.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>Re-anble ICMP traffic in the Network Security Group {NSG} for your ubuntu VM.</p>
<p>Return to the Windows 10 VM to monitor the ICMP traffic in wireshark and observe</p>
<p>the ping activity in the command line,wich should now resume fuctioning.once confirmed,stop the ping activity.</p>
<img src="https://i.imgur.com/HsdDqA3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h3 align="center;">
  Time to observe SSH traffic
</h3>
<p>In wireshark,set filter to display only SSH traffic.</p>
<p>From your Windows 10 VM establish an SSH connection to your Ubuntu VM using its Private IP adress.</p>
<p>Execute commands sush as 1s,pwd and others in the SSH session</p>
<p>Observe the SSH traffic activity in wireshark as the commands are executed,generating visible traffic pattern</p>
<br />
<p>Exit the SSH connection by tyoing 'exit' and pressing {return}</p>
<img src="https://i.imgur.com/e2y88Gd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<br />
<h3 align="center;">
  Next, we're going to observe DHCP Traffic
</h3>
<br />
<p>In Wireshark,apply a filter to display only DHCP traffic.</p>
<p>On your Windows 10 VM,use the command line to request a new IP adress by running ipconfig/renew.</p>
<p>Observe the DHCP traffic generated in Wireshark during the process.</p>
<img src="https://i.imgur.com/Qb6erVd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3 align="center;">
  Let's now observe our DNS traffic next
</h3>
<br />
<p> Back in Wireshark, filter for DNS traffic only.</p>
<p>On your Windows 10 VM,open the command line and run nslookup command</p>
<p>to look up the ip adresses for google.com and disney.com.</p>
<p>simultaneously,monitor Wireshark with a filter set to DNS traffic</p>
<p>to observe the DNS queries and responses generated during the process.</p>
<img src="https://i.imgur.com/LvHrFzx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3 align="center;">
  Finally, we will observe RDP traffic to finish up this tutorial
</h3>
<br />
<p> Back in Wireshark, filter for RDP traffic only using "tcp.port==3389".</p>
<p> You'll be seing a non-stop stream of traffic. Do you know why there is constant traffic in our tcp.port==3389?</p>
<p>The explanation is that RDP protocol continuously streams a live feed from one computer to another,wich results in constant traffic being transmitted.</p>
<img src="https://i.imgur.com/hiJGFPM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<br />
<p>Now that we're finished observing the network, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT! This will prevent you from incurring additional charges</p>
<p>Close your Remote Desktop connection and delete resource group created at the start of this tutorial.</p>
<p>Confirm the deletion by checking for a notification undeer the bell icon or waiting for confirmation message</p>
<p>to ensure the resource group have been successfully removed.</p>

