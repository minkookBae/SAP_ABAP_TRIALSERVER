# SAP_ABAP_TRIALSERVER
## Guide and manual for installing SAP ABAP trial server

<b>Reference : Customer Guide - Installing SAP AS ABAP 7.52 SP04 on VMWare [Developer Edition] Written by SAP</b>

Link : <span><a href="https://assets.cdn.sap.com/sapcom/docs/2019/09/c86f9218-687d-0010-87a3-c30de2ffd8ff.pdf"><u>Customer Guide</u></a></span>

## 0. Prerequisite (Hardware, OS criteria) - By Customer Guide and readme file

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

## 1. Sign-up at SAP Universal ID for downloading **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04**
Link : <span><a href="https://account.sap.com/core/login-native"><u>SAP Universal ID register page</u></a></span>

![][Image1]
![][Image2]

* Sign up for download (We'll skip specific sign-up step at this repository)

### 1.1 Download **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04** install files

![][Image3]

* Download above files all and extract rar file

I've extracted install file at 'install' directory like below.
![][Image4]

For us, The first difficulty things that downloading install file and license procedures for SAP installation are all finished.

## 2. Download VMware Workstation Player and OpenSUSE leap(linux OS)

> Download VMware Workstation Player, version 14.0 for your operating system

Link : <span><a href="https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_workstation_player/14_0"><u>Vmwarew Workstation Player 14.0</u></a></span>

![][Image5]
![][Image6]

> Download OpenSuSE leap(linux OS) ver 15.2

Link : <span><a href="https://get.opensuse.org/leap/15.2/"><u>openSUSE Leap 15.2</u></a></span>

![][Image7]

* When I try to install through 15.4 version, it doesn't go smoothly, so I'm making this guide based on 15.2 version.


[Image1]: /img/1_SAP_Register.png
[Image2]: /img/2_SAP_Register.png
[Image3]: /img/3_SAP_NW_download.png
[Image4]: /img/4_extract.png
[Image5]: /img/5_vmware_download.png
[Image6]: /img/6_vmware_download.png
[Image7]: /img/7_openSUSE_download.png