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

<h2>Actions and Observations</h2>

<p>
Create Resource Group
  
- Go to https://portal.azure.com/ once you have created a free account on Microsoft Azure.
- From there go onto the website's search bar and type "Resource Groups" in order to create a resource group.
- Name your resource group, and then choose a region based on your current location.
- Click "Review + create". A page will load, and you would click on "Create"

</p>

<p>
<img src="https://i.imgur.com/pwxyNmc.png" height="80%" width="80%" alt="Create Resource Group"/>
</p>

<hr>

<p>
Create Windows Virtual Machine  
  
- Next, on the search bar, search for "Virtual Machines" and click the result.
- Click on "Create" and choose the "Azure virtual machine" option
- Input the necessary details such as the resource group (the one you recently made), virtual machine name, and region. For <b>image*</b> choose "Windows 10 Pro" from the dropdown list.
- Scroll down to choose a <b>Size</b>. I would recommend an option with at least 2 vcpus, so your virtual machine doesn't run slow.</p>
- Input a username and password to log into the virtual machine. Then, click "Review + create". 

</p>

<p>
<img src="https://i.imgur.com/ihFTF6f.png" height="400" width="500" alt="Create Virtual Machine"/>
</p>

<hr>

<p>
Create Linux Virtual Machine
  
- Repeat most of the previous steps, but this time set <b>image*</b> to "Ubuntu Server 20.04 LTS".
- Also, for <b>Authentication type</b>, click on "Password" rather than "SSH public key".
- Setup your username and password. Then, click "Review + create". 

</p>
<p> </p>
<br />

<p>
Remote Desktop
  
- Open up "Microsoft Remote Desktop"
- On Windows, you can search it on a search bar that's located on the bottom-left of your computer screen. For other operating systems like Mac, you can find a "Microsoft Remote Desktop" app on the app store. 

</p>
<p> </p>
<br />

<p>
Logging into RD

- When you have the application opened, paste the "Public IP address" of your windows virtual machine. You can search for your virtual machines on the Azure search bar and see the ip address once you click on the name of your virtual machine.
- You should be able to find the public ip address towards the right of the screen.

</p>
  
<p>
<img src="https://i.imgur.com/nJZFm5c.png" height="80%" width="80%" alt="VM public ip address"/>
</p>

<hr>

<p>
Download Wireshark
  
- Once you have logged into the remote desktop with your username and password, open up "Microsoft Edge".
- From there, search up "wireshark download" and download it from the official website.

</p>
<img src="https://i.imgur.com/4jUormX.png" height="80%" width="80%" alt="wireshark download"/>

<hr>

<p>
Seeing Traffic
  
- Install and open the program</p>
- Click on "Ethernet" and then the "blue shark fin" icon. You should then see some traffic popping up in the software.

</p>
<img src="https://i.imgur.com/BcdpS8Y.png" height="80%" width="80%" alt="wireshark"/>

<hr>

<p>
ICMP Pinging
  
- Type "ICMP" and hit "Enter" on the filter bar. You'll notice that there's no traffic going on.
- Open up the command line. You can do this by typing "powershekk" on the search bar of the window's toolbar.
- Switch over to the Azure website and copy the private IP address of your Linux virtual machine. On powershell, type "ping [paste IP address]".
- Watch the ICMP traffic on Wireshark.

</p>
<img src="https://i.imgur.com/yyxVpoz.png" height="80%" width="80%" alt="icmp traffic"/>

<hr>

<p>
Google's Traffic
  
- In Powershell, this time, type "ping www.google.com"
- You'll notice traffic being sent between your ip address and Google's ip address.

</p>
<img src="https://i.imgur.com/YdNuqns.png" height="80%" width="80%" alt="ping traffic"/>

<hr>

<p>
Add A Deny Rule

- Type "ping [linux virtual machine's private ip address] -t", which creates non-stop traffic.
- Go back to the Azure site and search for "Network security groups"
- Click on [linux virtual machine-nsg] -> Inbound security rules
- Add a new rule
- Set "Protocol": ICMP, "Action": Deny, "Priority": 200, and "Name": Deny_Any_ICMP_Protocol</p>
- This new rule should time out the requests.

</p>
<img src="https://i.imgur.com/xKsbROx.png" height="80%" width="80%" alt="deny icmp"/>

<hr>

<p>
Edit Deny Rule
  
- Edit the newly made rule by setting "Action" to "Allow". This will resume the ping activity.

</p>
<img src="https://i.imgur.com/dBBH5BE.png" height="80%" width="80%" alt="allow icmp"/>

<hr>

<p>
SSH Traffic
  
- Filter for "ssh" on Wireshark
- Type "ssh [username of linux virtual machine]@[private ip address]" onto Powershell
- Enter the password you thought of during the time you made the linux machine. You can't see the actual characters when you type, but the characters are there.
- Watch the ssh traffic
- Type "exit" and press "enter" to exit the SSH connection

</p>
<img src="https://i.imgur.com/dBBH5BE.png" height="80%" width="80%" alt="ssh"/>

<hr>

<p>
DHCP Traffic
  
- Filter for "DHCP"</p>
- In Powershell, type "ipconfig /renew" to watch the DHCP traffic.

</p>
<img src="https://i.imgur.com/71stoFI.png" height="80%" width="80%" alt="dhcp"/>
<p> </p>
<br />

<hr>

<p>
DNS Traffic 
  
- Filter for "DNS", or in this case, "udp.port == 53"
- Type "nslookup www.disney.com" on Powershell
- Watch the DNS traffic
 
</p>
<img src="https://i.imgur.com/oYerTRM.png" height="80%" width="80%" alt="dhcp"/>

<hr>

<p>
RDP Traffic
  
- Filter for RDP using "tcp.port == 3389"
- Watch the non-stop traffic on Wireshark

</p>
<img src="https://i.imgur.com/ZsRJ2xj.png" height="80%" width="80%" alt="dhcp"/>

<hr>

<p>Close your remote desktop connection</p>
<p>On the Azure site, find your resource groups/virtual machines and delete them.</p>
