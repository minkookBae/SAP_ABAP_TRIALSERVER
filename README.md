# SAP_ABAP_TRIALSERVER
## Guide and manual for installing SAP ABAP trial server

<b>Reference : Customer Guide - Installing SAP AS ABAP 7.52 SP04 on VMWare [Developer Edition] Written by SAP</b>

Link : <span><a href="https://assets.cdn.sap.com/sapcom/docs/2019/09/c86f9218-687d-0010-87a3-c30de2ffd8ff.pdf"><u>Customer Guide</u></a></span>

## Prerequisite (Hardware, OS criteria) - By Customer Guide and readme file

> Customer Guide
* x86_64 Processor based hardware
* About 100 GB free disk space for server installation
* About 2 GB free disk space for client installation
* English – SAP AS ABAP requires that you configure English
    * (LANG=en_US.UTF-8) as the operating system language

> readme file
* x86_64 Processor based hardware
* At least 4 GB RAM plus about 8 GB swap space
* About 100 GB free disk space for server installation
* About 2 GB free disk space for client installation

## Preparation

### 1. Sign-up at SAP Universal ID for downloading **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04**
Link : <span><a href="https://account.sap.com/core/login-native"><u>SAP Universal ID register page</u></a></span>

![Image1]
![Image2]

* Sign up for download (We'll skip specific sign-up step at this repository)

### 2. Download **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04** install files and Extract them

![Image3]

* Download above files all and extract rar file

I've extracted install file at 'install' directory like below.
![Image4]

For us, The first difficulty things that downloading install files and license procedures for SAP installation are all finished.

### 3. Download VMware Workstation Player and openSUSE leap(linux OS) and other utility programs(winSCP)

> Download VMware Workstation Player, version 14.0 for your OS

Link : <span><a href="https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_workstation_player/14_0"><u>Vmwarew Workstation Player 14.0</u></a></span>

![Image5]
![Image6]

* Please note that you should not install version 15.0>= yet.

  There iscurrently an issue with version 15 and some versions of Windows (independent of AS ABAP). - customer guide


> Download OpenSuSE leap(linux OS) ver 15.2

Link : <span><a href="https://get.opensuse.org/leap/15.2/"><u>openSUSE Leap 15.2</u></a></span>

![Image7]

* When I try to install through 15.4 version, it doesn't go smoothly, so I'm making this guide based on 15.2 version.

> Download and Install WinSCP

Link : <span><a href="https://winscp.net/eng/download.php"><u>https://winscp.net/eng/download.php</u></a></span>
![Image8]

It is a convenient utility program for copying the ABAP installation files from local PC to the VM linux system.

## Create Virtual Machine With VMware Workstation

#### 1. Start VMware Player and create a new virtual machine by clicking 'Create a New Virtual Machine'
![Image9]
#### 2. Select Installer disc image file (iso) from local PC with Brose... button and choose Next
![Image10]
#### 3. Select Guest operating system and Vesion and choose Next
![Image11]
#### 4. Set the Virtual machine name and Location with yourself and choose Next
![Image12]
#### 4. **Set the Maximum disk size with 100 GB** and choose Next
![Image13]
#### 5. With Customize Hardware, **Change the Processors to 4 Number of processor cores and Memory to 8GB** and create VM instand with finish
![Image14]
#### 6. With 'Play virtual machine' button, Start the VM instance that has been made just before
![Image15]

#### 7. With keyboard(not mouse), select Installation option and press 'Enter'
![Image16]

#### 8. After several Linux installation procedures, set the Language and Keyboard Layout. Set it to English and proceed through the Next button.
![Image17]

#### 9. If you need to check 'Network Activation', please proceed with Next.
#### 10. Choose 'Desktop with GNOME' option and Next
![Image18]

#### 11. At Disk Partitioning step, we need to change partitioning option with Expert Partioner.
we can proceed with 'Start with Cur rent Proposal' Option.

![Image19]

![Image20]


And then, Choose /dev/sda2 Device and click 'Modify' -> 'Edit Partition'

![Image21]

After that, Change Filesystem format to Ext4 and Click next buttton, and Choose Accept.

#### 12. Seledct your Region and Timze zone and Next
![image22]

#### 13.  Enter : User's Full Name, Password
In this section, I've set the User name with 'ABAP', and password as well.
![image23]

#### 14. **Important : You need to make the following settings. Scroll down to find Firewall and SSH**:
1) Enable Firewall
2) Disable SSH service:

![image24]

#### 15. Click on Install and Confirm again to Install the Operating System.
> The Linux operating system will install in few minutes.

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