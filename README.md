<p align="center">
<img src="https://i.imgur.com/BqTgl08.png" alt="Virtualbox logo"/>
</p>

<h1>vOracle VirtualBox: VM Setup & Initial Configuration</h1>
<h2>Overview</h2>
This lab demonstrates how to create and configure a virtual machine using Oracle VirtualBox to prepare for a Windows Server installation.

The goal is to simulate a real-world environment where a system administrator provisions virtual infrastructure before deploying operating systems.<br />



<h2> Technologies Used</h2>

- Oracle VirtualBox (v7)
- Windows Server 2025 (ISO)
- Virtual Networking (NAT Network + DHCP)

<h2> System Requirements </h2>

- Host machine with virtualization enabled (VT-x / AMD-V)
- Minimum 8 GB RAM recommended
- Sufficient disk space (80 GB virtual disk)

<h2> Deployment and installation steps </h2>

<h3> 1. Start downloading Windows Server </h3>
Log in to Microsoft Azure Education with your Office365/Microsoft user. Open Learning Resources in the menu on the left and select Software.  Search for Windows Server. Find the product Windows Server 2025 Standard, and click it.

Click View Key in the column on the right, and copy the product key with the symbol. Use the Download button to download the file with the ISO Image with installation files. The file is large, so this will take some time.
<p>
<img src="https://i.imgur.com/PsWIeiD.jpeg" height="80%" width="80%" alt="Windows Sever Download steps"/>
</p>

<h3> 2. Install Oracle VM VirtualBox version 7 </h3>

If you have an older version of VirtualBox installed, you should download and install the latest version!
(All existing virtual machines will be preserved after the installation.)
- Download Oracle VM VirtualBox for your OS, and install locally on your machine.
-You should also download the Oracle VM VirtualBox Extension Pack from the same website.
You install this after VirtualBox is installed. The Extension Pack provides additional support in VB for newer
hardware technology.

-  Start Oracle VM VirtualBox and select <img src="https://i.imgur.com/4EhMRV3.png" height="10%" width="10%" alt=" expert mode"/>(This will make it easier to understand what you are doing). </p>
     <img src="https://i.imgur.com/h4RY1b0.png" height="70%" width="70%" alt="virtualbox "/>
     
 Note: For PC (not applicable to Mac): Make sure that Intel's/AMD's virtualization technology (VT-x/AMD-V) is
enabled in the BIOS/UEFI-Setup on your physical machine. See instructions on the last section of this
document.

Use the menu option File → Preferences… and the General tab.
 
 <img src="https://i.imgur.com/Nn92skA.png" height="50%" width="50%" alt=" file preferences "/>
 
Specify where you want to store the virtual machines in the Default Machine Folder field.
Feel free to create a new folder at the root level on a physical SSD disk, e.g. E:\MyVMs instead of E:\MineVmer like i did.
Each virtual machine will have its own subfolder under the folder specified here.
In the Language tab, you can optionally set a different language setting if you wish.


<h2> Network Configuration </h2>
<h3>Create a new virtual network with private IP addresses</h3>
Select the menu option File → Tools → Network and select the NAT Networks tab:
 <img src="https://i.imgur.com/zawhlBS.png" height="50%" width="50%" alt=" private ip adresses"/>

 Add a new NAT network using the Create button.
The network can be named NatNetwork as VB suggests.
<img src="https://i.imgur.com/H5KiHBQ.png" height="50%" width="50%" alt="NatNetwork"/>

Open the properties window for the new network with the "Properties button".
<img src="https://i.imgur.com/VPvik9S.png" height="50%" width="50%" alt="properties"/>

Make sure that the Enable DHCP field is active/on. This activates the DHCP server in VirtualBox so that it automatically distributes IP addresses to the virtual machines in the virtual network.
- This lab is based on the virtual network using IP addresses in the range
192.168.52.0 to 192.168.52.255. You enter this as 192.168.52.0/24 in the IPv4 Prefix field as
shown in the image above.
- The Enable IPv6 field should be unchecked. We will not use IPv6 in this topic.
- Click Apply to save the new network.
- Return to the Home page
<img src="https://i.imgur.com/IqT4Ehc.png" height="50%" width="50%" alt="properties"/>


<h2> Virtual Machine Creation for Windows Server</h2>

The images below are taken from . In Guided mode you get the same options on multiple "pages".
Create a new virtual machine with the menu option Machine → New… (Ctrl-N). 

<img src="https://i.imgur.com/bvvYkdm.png" height="50%" width="50%" alt="properties"/>
  
 - Name the virtual machine Server_VM.
- Select Other… in the ISO Image field and find the ISO file with the installation files for Windows
Server on local (physical) disk. (The one you downloaded from Microsoft Azure Education.)
-  Turn OFF the Proceed with Unattended Installation field !!!
This ensures that VirtualBox does not start an automated installation of Windows Server,
and allows you to change several options in the image.
- Select Microsoft Windows in the OS field (i.e. the guest operating system for the VM).
- Select Windows 2025 (64-bit) in the OS Version field
Note: If you only see 32-bit OS versions in this list, you must enable Intel's / AMD's
virtualization technology in BIOS Setup. See the recipe at the very end of this document.

Note: If you only see 32-bit OS versions in this list, you must enable Intel's / AMD's
virtualization technology in BIOS Setup. See the recipe at the very end of this document

Open the Specify virtual hardware row

<img src="https://i.imgur.com/Slv4Xcw.png" height="50%" width="50%" alt="properties"/>

- Select 2-4 GB of internal memory (Base Memory)
- Select 2-4 CPUs in the Processors field

Notes: If your physical machine has a lot of internal memory (16+ GB RAM), you can give the VM 3-4 GB. If you have limited physical RAM (< 8 GB), you can also run Windows Server with 1-2 GB RAM, but it will probably be a bit slower. Remember that you will be using two VMs at the same time in several of the exercises.
2 CPUs are enough for this lab, but if you have a physical machine with many processor cores, you can increase this value slightly.

 
Open the row Specify virtual hard disk
Select Create a Virtual Hard Disk Now
<img src="https://i.imgur.com/fZyIxGw.png" height="50%" width="50%" alt="properties"/>

- Name the file with the virtual disk: Server_VM_disk0.vdi
- Select 80 GB as the disk size. (Note: VB does not use all of this physically, but only as much
physical disk space as it actually needs.)
- Select 80 GB as the disk size. (Note: VB does not use all of this physically, but only as much
physical disk space as it actually needs.)
- Select VDI (VirtualBox Disk Image) in the Hard Disk File Type and Format field
- The Pre-allocate Full Size field must be unchecked.
(otherwise the entire disk size will be reserved on the physical disk immediately)

Create the VM with the Finish button

VirtualBox will now build the VM for you, and it will be visible in the VirtualBox Manager as shown below.

<img src="https://i.imgur.com/SWtQjxA.png" height="80%" width="80%" alt="properties"/>

<h2> Hardware Configuration of Virtual Machine</h2>
<p>Select the new VM and use the Settings button <img src="https://i.imgur.com/nyyrdgV.png" height="5%" width="5%" alt="properties"/> </p> 

Select General and then the Features tab

 Set Shared Clipboard to Bidirectional.                            
This allows you to cut and paste
between the physical and virtual machine. (Requires
the VirtualBox Extension Pack to be installed.)     <p><img src="https://i.imgur.com/1Wn44OL.png" height="60%" width="60%" alt="properties"/> </p> 

Select System and the Motherboard tab

- Set Boot Order as shown on the right and uncheck Floppy
- Set Chipset* to ICH9
- Set TPM* to v2.0
- Set Pointing Device to the type of mouse you have on your own physical machine.
- The Chipset and TPM choices are more "modern" hardware than the default values ​​that
<p><img src="https://i.imgur.com/dNmHByv.png" height="60%" width="60%" alt="properties"/> </p> 

VirtualBox suggests. Windows Server 2025 requires this hardware.

Select Network and the Adapter 1 tab

- Enable Network Adapter should be on.
- Set Attached to to NAT Network
- Select NatNetwork in the Name field
(The virtual network you created in task b)
<p><img src="https://i.imgur.com/JnAaz8G.png" height="60%" width="60%" alt="properties"/> </p> 


Click OK

<p>After the virtual machine is created and configured, you can start the VM using the Start button. The virtual machine will then boot from the Windows Server ISO image file and automatically launch the Windows Server installer..<img src="https://i.imgur.com/9C4UuUq.png" height="5%" width="5%" alt="properties"/> </p> 



<h2> Extra info: Check that Intel/AMD virtualization is enabled in BIOS/UEFI Setup</h2>
To run virtual machines, special virtualization technology built into the physical machine's processor (CPU) is required. Processor manufacturers Intel and AMD call their technologies VT-x and AMD-V, respectively.

On machines intended for "personal use" (especially laptops), this feature is often turned off by default. In that case, you must start the machine's BIOS/UEFI Setup program at startup and turn this option on.

You usually start the BIOS/UEFI Setup program with a function key while the physical machine is booting up, and before Windows starts! Often, you should press the F2 or F12 key during startup, but this can vary for each machine type. If you don't know how to do this on your machine, you can find it in the machine's instruction manual (which is easy to Google).
When you enter BIOS/UEFI Setup, the relevant options are usually under "Advanced
settings" and/or "CPU/processor setup".

Here's what the BIOS settings look like on a newer Dell machine:
<p><img src="https://i.imgur.com/Gvtyev6.png" height="60%" width="60%" alt="properties"/> </p> 

This is what the BIOS settings look like on a slightly older Lenovo machine:
<p><img src="https://i.imgur.com/L4BfdwE.png" height="60%" width="60%" alt="properties"/> </p> 

You can read more about this topic on https://support.lenovo.com/my/en/solutions/ht500006 and its important to make sure this is enabled before you begin following the steps to this lab. 

