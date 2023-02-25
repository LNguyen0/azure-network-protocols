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

<p>Go to https://portal.azure.com/ once you have created a free account on Microsoft Azure.</p>
<p>From there go onto the website's search bar and type "Resource Groups" in order to create a resource group.</p>
<p>Name your resource group, and then choose a region based on your current location.</p>
<p>Click "Review + create". A page will load, and you would click on "Create"</p>

<p>
<img src="https://i.imgur.com/pwxyNmc.png" height="80%" width="80%" alt="Create Resource Group"/>
</p>

<br />
<p> </p>
<p>Next, on the search bar, search for "Virtual Machines" and click the result.</p>
<p>Click on "Create" and choose the "Azure virtual machine" option </p>
<p>Input the necessary details such as the resource group (the one you recently made), virtual machine name, and region. For <b>image*</b> choose "Windows 10 Pro" from the dropdown list.</p>
<p>Scroll down to choose a <b>Size</b>. I would recommend an option with at least 2 vcpus, so your virtual machine doesn't run slow.</p>
<p>Input a username and password to log into the virtual machine. Then, click "Review + create". </p>

<p>
<img src="https://i.imgur.com/ihFTF6f.png" height="400" width="500" alt="Create Virtual Machine"/>
</p>
<p> </p>
<br />

<p>Create another virtual machine, but this time set <b>image*</b> to "Ubuntu Server 20.04 LTS".</p>
<p>Also, for <b>Authentication type</b>, click on "Password" rather than "SSH public key".</p>
<p>Setup your username and password. Then, click "Review + create". 
<p> </p>
<br />

<p>Open up "Microsoft Remote Desktop". </p>
<p>On Windows, you can search it on a search bar that's located on the bottom-left of your computer screen. For other operating systems like Mac, you can find a "Microsoft Remote Desktop" app on the app store. </p>
<p> </p>
<br />

<p>When you have the application opened, paste the "Public IP address" of your windows virtual machine. You can search for your virtual machines on the Azure search bar and see the ip address once you click on the name of your virtual machine.</p>
<p>You should be able to find the public ip address towards the right of the screen.</p>
  
<p>
<img src="https://i.imgur.com/nJZFm5c.png" height="80%" width="80%" alt="VM public ip address"/>
</p>
<p> </p>
<br />

<p>Once you have logged into the remote desktop with your username and password, open up "Microsoft Edge".</p>
<p>From there, search up "wireshark download" and download it from the official website.</p>
<img src="https://i.imgur.com/4jUormX.png" height="80%" width="80%" alt="wireshark download"/>
<p> </p>
<br />

<p>Install and open the program.</p>
<p>Click on "Ethernet" and then the "blue shark fin" icon. You should then see some traffic popping up in the software.</p>
<img src="https://i.imgur.com/BcdpS8Y.png" height="80%" width="80%" alt="wireshark"/>
<p> </p>
<br />

<p>Type "ICMP" and hit "Enter" on the filter bar. You'll notice that there's no traffic going on.</p>
<p>Open up the command line. You can do this by typing "powershekk" on the search bar of the window's toolbar.</p>
<p>Switch over to the Azure website and copy the private IP address of your Linux virtual machine. On powershell, type "ping [paste IP address]".</p>
<p>Watch the ICMP traffic on Wireshark.</p>
<img src="https://i.imgur.com/yyxVpoz.png" height="80%" width="80%" alt="icmp traffic"/>
<p> </p>
<br />
