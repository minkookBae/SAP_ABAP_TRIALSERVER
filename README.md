# SAP ABAP Trial Server

## Guide and Manual for Installing SAP ABAP Trial Server

**Reference:** Customer Guide - Installing SAP AS ABAP 7.52 SP04 on VMware [Developer Edition] Written by SAP

You can refer to another language version: [**한국어**](/ko/README_ko.md)

**Link:** [Customer Guide](https://assets.cdn.sap.com/sapcom/docs/2019/09/c86f9218-687d-0010-87a3-c30de2ffd8ff.pdf)

## Prerequisite (Hardware, OS Criteria) - By Customer Guide and Readme File

### Customer Guide
- x86_64 Processor-based hardware
- About 100 GB free disk space for server installation
- About 2 GB free disk space for client installation
- English – SAP AS ABAP requires that you configure English:
  - `LANG=en_US.UTF-8` as the operating system language

### Readme File
- x86_64 Processor-based hardware
- At least 4 GB RAM plus about 8 GB swap space
- About 100 GB free disk space for server installation
- About 2 GB free disk space for client installation

## Preparation

### 1. Sign Up at SAP Universal ID for Downloading **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04**
**Link:** [SAP Universal ID Register Page](https://account.sap.com/core/login-native)

![Image1]
![Image2]

- Sign up for download (We'll skip specific sign-up steps in this repository).

### 2. Download **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04** Install Files and Extract Them

![Image3]

- Download all the above files and extract the `.rar` file.

I've extracted the install file into the `install` directory as shown below:

![Image4]

For us, the first difficulty—downloading install files and license procedures for SAP installation—is already completed.

### 3. Download VMware Workstation Player, openSUSE Leap (Linux OS), and Other Utility Programs (WinSCP)

#### VMware Workstation Player
- Download VMware Workstation Player, version 14.0 for your OS: [VMware Workstation Player 14.0](https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_workstation_player/14_0)

![Image5]
![Image6]

- **Note:** Do not install version 15.0 or higher yet. There is currently an issue with version 15 and some versions of Windows (independent of AS ABAP). - Customer Guide

#### openSUSE Leap (Linux OS) Version 15.2
- Download openSUSE Leap 15.2: [openSUSE Leap 15.2](https://get.opensuse.org/leap/15.2/)
- [openSUSE Leap 15.2 Download Page](http://download.opensuse.org/distribution/leap/15.2/iso/)

**File Name:** `openSUSE-Leap-15.2-DVD-x86_64.iso`

![Image7]

- **Note:** When I tried to install version 15.4, it didn't go smoothly, so this guide is based on version 15.2.

#### WinSCP
- Download and install WinSCP: [WinSCP Download](https://winscp.net/eng/download.php)

![Image8]

WinSCP is a convenient utility program for copying the ABAP installation files from a local PC to the VM Linux system.

## Create Virtual Machine With VMware Workstation

### 1. Start VMware Player and create a new virtual machine by clicking 'Create a New Virtual Machine'
![Image9]
### 2. Select Installer disc image file (iso) from local PC with Browse... button and choose Next
![Image10]
### 3. Select Guest operating system and Version and choose Next
![Image11]
### 4. Set the Virtual machine name and Location with yourself and choose Next
![Image12]
### 5. **Set the Maximum disk size with 100 GB** and choose Next
![Image13]
### 6. With Customize Hardware, **Change the Processors to 4 Number of processor cores and Memory to 8GB** and create VM instance with finish
![Image14]
### 7. With 'Play virtual machine' button, Start the VM instance that has been made just before
![Image15]

### 8. With keyboard (not mouse), select Installation option and press 'Enter'
![Image16]

### 9. After several Linux installation procedures, set the Language and Keyboard Layout. Set it to English and proceed through the Next button.
![Image17]

### 10. If you need to check 'Network Activation', please proceed with Next.
### 11. Choose 'Desktop with GNOME' option and Next
![Image18]

### 12. At Disk Partitioning step, we need to change partitioning option with Expert Partitioner.
we can proceed with 'Start with Current Proposal' Option.

![Image19]

![Image20]

And then, Choose /dev/sda2 Device and click 'Modify' -> 'Edit Partition'

![Image21]

After that, Change Filesystem format to Ext4 and Click next button, and Choose Accept.

### 13. Select your Region and Time zone and Next
![image22]

### 14. Enter: User's Full Name, Password
In this section, I've set the User name with 'ABAP', and password as well.
![image23]

### 15. **Important: You need to make the following settings. Scroll down to find Firewall and SSH**:
1) Enable Firewall
2) Disable SSH service:

![image24]

### 16. Click on Install and Confirm again to Install the Operating System.
> The Linux operating system will install in a few minutes.

## Setup openSUSE VM Instance for ABAP Installation

### In this section, we'll make some settings in the openSUSE system to prepare ABAP Installation

- Change proxy settings
- Download and extract the ABAP .rar files
- Install the uuidd daemon
- Edit the hostname and hosts files
- Assign root privileges to the install script

### 1. After Installation openSUSE OS, Boot VM Instance
![image25]

### 2. Check the memory storage is enough or not.
> Execute Terminal and execute shell script.

![image26]
```
df -h
```
![image27]

### 3. Download uuidd, tcsh, unrar utility program from terminal with below shell script
If you counter Y/N choice, put the 'Y' and press Enter button.

```
sudo zypper install uuidd
sudo zypper install tcsh
sudo zypper install unrar
```

> uuidd daemon: This daemon provides universal unique identifiers – essential for creating database keys. (See SAP Note [1310037](https://launchpad.support.sap.com/#/notes/1310037) for more details.)

> tcsh: program for executing install.sh afterward

> unrar: program for unzip rar files (the files format we have downloaded from SAP page)

### 4. Change the Proxy settings, if you are behind a proxy
I'll skip this section because I'm not behind a proxy.
If you want to set it, please refer Customer guide.

### 5. Set DHCP Settings to NO
In YaST > System > Network Settings > Set Hostname via DHCP = No
![image28]

### 6. Start uuidd daemon with shell script and also we need to check libaio or libaio1 is installed on your Linux system

```
sudo service uuidd start
sudo service --status-all | grep uuidd
rpm -qa | grep libaio
```

![image29]

### 7. Edit the hostname and hosts files
by entering sudo vi /etc/hostname, we can change hostname to '**vhcalnplci**'
```
sudo vi /etc/hostname
```

After changing it, we can check the hostname and restart network by entering sudo rcnetwork restart
```
sudo rcnetwork restart
```
And Restart your linux instance and check that the hostname has changed to '**vhcalnplci**'

![image30]

### 8. Map the IP Address to the new hostname:
We can find IP address with IP address command
```
ip address
```
![image31]

Open the host files by entering sudo vi /etc/hosts
Using this IP address, add a new entry of the form

```
sudo vi /etc/hosts

<IP address> <hostname> <hostname>.dummy.nodomain
<IP address> vhcalnplci vhcalnplci.dummy.nodomain
```
![image32]

Check the changes by using the command sudo cat /etc/hosts

```
cat /etc/hosts
```

### 9. Copy the ABAP files using WinSCP

Using IP Address above, we can access SFTP via WinSCP program.
I've made a new directory 'ABAP' and copy all extracted data to that directory (without client directory)

> All extracted files will be copied to VM in a few minutes.

![image33]

**We need to Change License file manually**

From the extracted 'License' directory, there is a 'SYBASE_ASE_TestDrive.lic' file.

We need to copy to VM Instance directory **'/server/TAR/x86_64/SYBASE_ASE_TD.lic'** (file name should be changed)

If there is SYBASE_ASE_TD.lic file already, overwrite it.
![image34]

> Add: April 27, 2023.

> In case of you are using previous license version which is valid until March, 2023,
And such case of you have already installed NPL system, **you need to update to a recently distributed license**.

![image40]

Guide: You can refer this [link page](https://pawelwiejkut.dev/posts/npl-wont-start/)

### 10. Assign root privileges
Change the access rights of the install script:
```
sudo -i
chmod +x install.sh
```
![image35]

## INSTALL THE AS ABAP SERVER

> Finally, we can run installation script by entering
```
./install.sh
```
1. Read and accept the license agreement (167 lines). To escape from the License Agreement, choose “Esc” followed by “:q”.
2. When prompted for the OS user’s password enter your master password of the virtual Linux OS instance twice
3. Be patient, this will take a while…
4. If the installation is successful, you will see something like this:

![image36]

## Getting started

> Starting and stopping the server

> To start the SAP system:
1. Switch to user npladm with default password in the console: su npladm
```
su npladm
```

2. To start the SAP system, enter startsap
```
startsap
```
3. To stop the SAP system, switch to user npladm and enter stopsap.
```
stopsap
```

## Install SAP GUI For Windows
You can install SAP GUI For Windows at the <install_folder>\client\SAPGUI4Windows\50144807_6.ZIP

In the extracted archive, navigate to …PRES1\GUI\Windows\Win32\SetupAll.exe and run it, following the instructions in the Wizard.

![image37]

## Connecting to the ABAP server from SAP GUI for Windows

> To connect to the ABAP server using SAP GUI for Windows:

1. Navigate to your Windows hosts file: C:\Windows\System32\drivers\etc\hosts.
2. Open this file in Administrator mode and add the following lines:

```
<ip_address> vhcalnplci vhcalnplci.dummy.nodomain
```

3. In the SAP Logon pad, choose New > Connection:
4. Choose User-specific system and enter the following, entering your own IP address:

• Application server = <ip_address>

• Instance = 00

• System ID = NPL

![image38]

## ABAP License Key
1. Start the SAP System and create a SAP GUI connection as above.
2. Log on to the system with the client 000 and user **SAP*** with default password **Down1oad**
. In transaction SLICENSE, note down or copy your Active Hardware Key.
3. Request the license key for your trial version at [SAP License Keys for Preview, Evaluation and Developer Versions](https://go.support.sap.com/minisap/#/minisap)

NOTE: Do not use the link in the transaction SLICENSE in the panel Request License Key.

a) Select NPL – SAP NetWeaver 7.x (Sybase ASE) as System ID.

![image39]

b) Enter your personal data and agree to the License Agreement.

c) Choose Generate bottom right corner of screen.

d) The web site automatically generates a .txt file for this system/key. Download and save this file, eg on the desktop for convenience.

4. Go to transaction SLICENSE and install the license file:

a) In the tab Digitally signed licenses, delete the existing license, then choose Install. This opens the text file you got and installs the new license key.

Please note that all the above steps must be carried out; otherwise, the above user key will
not work.

The system type changes to Demo. You can now explore the demo scenarios and develop using the ABAP tools in Eclipse and new features like the core data services or SAPUI5 UIs.

[Image1]: /img/1_SAP_Register.png
[Image2]: /img/2_SAP_Register.png
[Image3]: /img/3_SAP_NW_download.png
[Image4]: /img/4_extract.png
[Image5]: /img/5_vmware_download.png
[Image6]: /img/6_vmware_download.png
[Image7]: /img/7_openSUSE_download.png
[Image8]: /img/8_winscp_download.png
[Image9]: /img/9_vmware_create.png
[image10]: /img/10_vmware_create.png
[image11]: /img/11_vmware_create.png
[image12]: /img/12_vmware_create.png
[image13]: /img/13_vmware_create.png
[image14]: /img/14_vmware_create.png
[image15]: /img/15_vmware_install.png
[image16]: /img/16_vmware_install.png
[image17]: /img/17_vmware_install.png
[image18]: /img/18_vmware_install.png
[image19]: /img/19_vmware_install.png
[image20]: /img/20_vmware_install.png
[image21]: /img/21_vmware_install.png
[image22]: /img/22_vmware_install.png
[image23]: /img/23_vmware_install.png
[image24]: /img/24_vmware_install.png
[image25]: /img/25_vmware_setup.png
[image26]: /img/26_vmware_setup.png
[image27]: /img/27_vmware_setup.png
[image28]: /img/28_vmware_setup.png
[image29]: /img/29_vmware_setup.png
[image30]: /img/30_vmware_setup.png
[image31]: /img/31_vmware_setup.png
[image32]: /img/32_vmware_setup.png
[image33]: /img/33_vmware_setup.png
[image34]: /img/34_vmware_setup.png
[image35]: /img/35_vmware_setup.png
[image36]: /img/36_vmware_setup.png
[image37]: /img/37_sapgui.png
[image38]: /img/38_vmware_setup.png
[image39]: /img/39_license.png
[image40]: /img/40_new%20license.png