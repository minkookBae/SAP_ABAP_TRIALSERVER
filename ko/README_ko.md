# SAP_ABAP_TRIALSERVER
## SAP ABAP trial server 설치 가이드 문서(한글)
<b>참조문서 : Customer Guide - Installing SAP AS ABAP 7.52 SP04 on VMWare [Developer Edition] Written by SAP</b>

### 영문 버전으로 우선 작성하고 이후 한국어 번역하여 번역투가 강한 점 양해 부탁드립니다.

링크 : <span><a href="https://assets.cdn.sap.com/sapcom/docs/2019/09/c86f9218-687d-0010-87a3-c30de2ffd8ff.pdf"><u>가이드 문서</u></a></span>

## 사전 요구사항(하드웨어, OS 등) - 가이드 문서 기반

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

## 설치 준비 ( SAP 포탈 가입 및 파일 다운로드 등)

### 1. SAP universal ID 회원가입 및 **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04** 인스톨 파일 다운로드
링크 : <span><a href="https://account.sap.com/core/login-native"><u>SAP Universal ID 회원가입 페이지</u></a></span>

![Image1]
![Image2]

* 회원가입 등을 진행해주시면 됩니다. 기본적인 사항이라 해당 가이드에서는 스킵합니다.

### 2. **SAP NetWeaver AS ABAP Developer Edition 7.52 SP04** 파일 다운로드 및 압축 해제

![Image3]

* 위 파일 모두 다운로드 후 rar 파일 압축 해제해주세요.
가이드 문서에서는, 위와 같이 'install' 폴더 생성 후 압축해제 하였습니다.
![Image4]

### 3. 유틸리티 프로그램 다운로드 : VMware Workstation Player, openSUSE leap(linux os), WinSCP

> OS버전에 맞는 VMware Workstation Player 버전 14.0 다운로드

링크 : <span><a href="https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_workstation_player/14_0"><u>Vmware Workstation Player 14.0</u></a></span>

![Image5]
![Image6]

* 15.0 이상 버전의 VMware는 다운로드 받지 마세요!


> openSUSE leap(linux OS) ver 15.2 다운로드

링크 : <span><a href="https://get.opensuse.org/leap/15.2/"><u>openSUSE Leap 15.2</u></a></span>

다운로드 링크 : <a href="http://download.opensuse.org/distribution/leap/15.2/iso/"><u>openSUSE Leap 15.2 다운로드 페이지</u></a>

> 파일 명 : openSUSE-Leap-15.2-DVD-x86_64.iso

![Image7]

* 15.4 이후 버전으로 설치를 시도해보았었는데 오류가 난 적이 있어서.. 15.2 버전으로 가이드 문서를 작성 합니다.

> WinSCP 유틸리티 프로그램 다운로드 및 설치

링크 : <span><a href="https://winscp.net/eng/download.php"><u>https://winscp.net/eng/download.php</u></a></span>
![Image8]

로컬 PC에서 VM linux 인스턴스로 ABAP 인스톨 파일을 간단하게 전송하기 위한 유틸리티 프로그램입니다.

## VMware Workstation을 통한 VM 생성하기

#### 1. VMware Player를 실행 후 'Create a New Virtual Machine' 버튼을 통해 신규 VM을 생성합니다.

![Image9]
#### 2. Installer disc image file (iso) 를 선택 및 로컬 PC에서 앞서 다운로드 받는 linux iso 파일을 선택 후 다음 버튼을 클릭합니다.

![Image10]
#### 3. Guest operating system : Linux, Version은 openSUSE 64-bit을 선택 후 다음 버튼을 클릭합니다.

![Image11]
#### 4. VM 이름과 해당 VM 물리파일이 저장될 위치를 선택합니다.(기본으로 두셔도 무방합니다.)

![Image12]
#### 5. **Maximum disk size를 100GB로 조정**하고 다음 버튼을 누릅니다.

![Image13]
#### 6. Customize Hardware 탭에서는 프로세서를 4코어로, 메모리를 8GB로 변경 후 finish 버튼을 누릅니다.

![Image14]
#### 7. 'Play virtual machine' 버튼을 통해서 방금 생성한 VM을 실행합니다.

![Image15]
#### 8. 마우스로는 조작이 불가능하고, 키보드로 'Installation' 옵션을 선택 후 엔터 버튼 클릭

![Image16]
#### 9. 몇몇 설정이 자동으로 될 거고, 언어 설정이 나오면 English로 설정되어 계실 텐데, 바로 다음 버튼을 눌러 주시면 됩니다.

![Image17]
#### 10. 'Network Activation' 부분이 나오면 다음 버튼으로 진행해주시면 됩니다.

#### 11. 'Desktop with GNOME' 옵션을 누르고, 다음 버튼 통해 진행
![Image18]
#### 12. Disk Partitioning 단계에서는, Disk Partitioning 옵션을 조금 바꿔 주어야 합니다.

'Start with Current Proposal' 옵션을 통해 진행합니다.
![Image19]

![Image20]

그리고, /dev/sda2 저장장치를 누르고, Modify -> Edit Partition을 눌러주세요.

![Image21]

이후, Filesystem을 Ext4로 바꿔주시고 다음, Accept 하시면 되겠습니다.

#### 13. Region과 Timezone을 설정 후 다음
![image22]

#### 14. Linux 계정의 ID, PW를 설정합니다.
해당 가이드에서는 간단하게 ID를 ABAP 으로 설정하였습니다. 아무거나 설정해도 무방합니다.
![image23]
#### 15. 셋팅 완료 전, **Firewall과 SSH 셋팅을 변경해주어야 합니다.**

1) Enable Firewall
2) Disable SSH service:

![image24]

#### 16. Install 버튼 클릭 및 확인하여 OS 를 설치하면 됩니다!
> 새 OS 셋팅 및 설치를 진행하는 거라 PC 사양에 따라 상이하지만, 오랜 시간이 소요 되겠습니다.


## ABAP 서버 설치를 위한 opsnSUSE VM Instance 설정 

### 이번 섹션에서는 크게, ABAP 서버 설치 준비를 위해 아래와 같은 작업을 진행하도록 하겠습니다.

* 프록시 셋팅 변경
* ABAP .rar 파일 다운로드 및 파일 추출
* uuidd daemon 유틸리티 설치
* VM hostname과 hosts 파일 수정
* 설치 스크립트에 root 권한 부여

#### 1. openSUSE OS 설치 이후, VM Instance를 실행
![image25]

#### 2. 메모리 용량이 충분하지 확인
> 터미널 실행 후 아래 쉘 스크립트를 실행

![image26]
```
df -h
```
![image27]


#### 3. 아래 쉘 스크립트 통해 uuidd, tcsh, unrar 유틸리티 프로그램 설치
Y/N 선택지가 나오면, 'Y'를 넣으신 뒤 엔터 누르시면 되겠습니다.

```
sudo zypper install uuidd
sudo zypper install tcsh
sudo zypper install unrar
```



> uuidd daemon : 이 데몬은 데이터베이스 키를 만드는 데 필수적인 범용 고유 식별자를 제공합니다. (자세한 내용은 SAP Note <a href="https://launchpad.support.sap.com/#/notes/1310037">1310037</a>을 참조하십시오.)

> tcsh : 추후 실행할 install.sh 쉘 스크립트를 실행하기 위한 프로그램

> unrar : rar 파일(SAP page에서 다운로드 받은 파일 형식) 데이터 추출을 위한 유틸리티 프로그램

#### 4. 네트워크가 프록시 셋팅 내에 있다면, 프록시 셋팅을 변경
해당 가이드 작성자는 프록시 셋팅이 없어서, 스킵하도록 하겠습니다.
설정이 필요하시다면 Customer Guide를 참고하시기 바랍니다.

#### 5. DHCP setting을 'NO' 로 설정
YaST > System > Network Settings > Set Hostname via DHCP를 'No'로 셋팅
![image28]

#### 6. 아래 쉘 스크립트를 통해 uuidd daemon을 실행하고, 리눅스 시스템 내에 libaio(libaio1) 프로그램이 설치되어 있는지 확인

```
sudo service uuidd start
sudo service --status-all | grep uuidd
rpm -qa | grep libaio
```

![image29]


#### 7. hostname과 hosts 파일을 수정

sudo vi /etc/hostname을 입력해서 vim 내에서 hostname을 '**vhcalnplci**'로 변경할 수 있습니다.

```
sudo vi /etc/hostname
```

변경 후, hostname 확인 가능하고, 'sudo rcnetwork restart' 명령어 통해 네트워크 재실행 하시면 됩니다.

```
sudo rcnetwork restart
```
Linux 인스턴스를 재시작하고 hostname이 '**vhcalnplci**'로 변경되었는지 확인합니다.

![image30]

#### 8. 신규 Hostname에 IP 주소를 매핑
'ip address' 명령어로 IP 주소를 확인할 수 있습니다.
```
ip address
```
![image31]

'sudo vi /etc/hosts/' 명령어 통해서 hosts 파일을 vim으로 열고, 앞서 확인한 IP 주소를 아래 form에 맞게 입력하시면 되겠습니다.

```
sudo vi /etc/hosts

<IP address> <hostname> <hostname>.dummy.nodomain
<IP address> vhcalnplci vhcalnplci.dummy.nodomain
```
![image32]

'sudo cat /etc/hosts' 명령어 통해서 변경 사항을 확인하세요.

```
cat /etc/hosts
```

#### 9. WinSCP 유틸리티 통해서 ABAP 설치 파일을 복사

위에서 확인한 IP 주소를 통해서, WinSCP 프로그램을 사용해 SFTP 접속을 할 수 있습니다.

가이드 작성 시 'ABAP' 디렉터리를 새로 만들고, 모든 설치 파일을 복사했습니다.

> 설치 파일들의 VM 인스턴스 복사는 몇 분 정도 걸릴 수 있습니다.

![image33]

<u>**설치 License 파일을 수기로 바꾸어 주어야 합니다.**</u>

'License' 디렉터리를 확인해보시면 'SYBASE_ASE_TestDrive.lic' 파일이 존재하고,

해당 파일을 **'/server/TAR/x86_64/SYBASE_ASE_TD.lic'** 디렉터리 및 파일명으로 복사해 넣으시면 됩니다.

SYBASE_ASE_TD.lic 파일이 이미 있을테니, 덮어쓰기 하세요.
![image34]

#### 10. 루트 권한 부여
아래 쉘 스크립트를 통해서 설치 스크립트 파일의 file 권한을 변경하세요
```
sudo -i
chmod +x install.sh
```
![image35]

## ABAP SERVER 설치하기

> 드디어! 설치 스크립트를 실행할 준비가 다 되었습니다. 아래 쉘 스크립트를 실행하세요!

```
./install.sh
```


1. license agreement 내용(167줄)을 읽고 동의합니다. 내용에서 빠져나오시려면 "Esc" 를 누르신다음에 ":q"를 입력하세요.

2. OS 사용자 암호를 입력하라는 메시지가 나타나면 Linux OS 인스턴스의 암호를 입력하세요.

3. 설치에는 상당 시간이 소요됩니다. 

4. 설치가 성공적으로 완료되면, 아래 내용처럼 설치 완료 메시지를 볼 수 있습니다.

![image36]

## 시작하기

> 서버 구동과 중지 방법

> SAP system 구동하기

1. 터미널 내에서 'su npladm' 명령어 통해서 'npladm' 계정으로 바꾸기

```
su npladm
```

2. SAP system 구동을 위해 'startsap' 명령어 입력
```
startsap
```

3. SAP system 중지를 위해서는, 'npladm' 유저로 변경하고 'stopsap' 명령어 입력

```
stopsap
```


## SAP GUI 설치하기 - Windows OS 사용자

<install_folder>\client\SAPGUI4Windows\50144807_6.ZIP
에서 SAP GUI for windows 버전을 설치할 수 있습니다.

…PRES1\GUI\Windows\Win32\SetupAll.exe 에 있는 설치파일을 실행하고, 설치 마법사를 진행하시면 되겠습니다.

![image37]

## SAP GUI에서 ABAP Server로 연결하기

> SAP GUI에서 ABAP Server로 연결하기 위해

1. C:\Windows\System32\drivers\etc\hosts Windows 디렉터리에서 hosts파일 확인 후,

2. 해당 파일을 관리자 권한으로 실행하신 뒤에 아래 처럼 line을 추가하세요.

```
<ip_address> vhcalnplci vhcalnplci.dummy.nodomain
```

3. SAP GUI를 실행 후, SAP Logon 패드에서 New > Connection을 선택하시고

4. User-specific system을 선택 후 아래처럼 입력 하시면 되겠습니다.

• Application server = <ip_address>

• Instance = 00

• System ID = NPL

![image38]

## ABAP 개발자 라이센스 키 다운받기
1. SAP System 실행 후 기존 안내 대로 SAP GUI에서 connection을 생성

2. 클라이언트 000 및 사용자 **SAP***를 기본 암호 **Down1oad**로 입력하여 신규 시스템에 로그인합니다 이후, T-code : SLICENSE에서 활성 하드웨어 키를 저장하거나 복사합니다.

3. <a href="https://go.support.sap.com/minisap/#/minisap"><u>SAP License Keys for Preview, Evaluation and Developer Versions</u></a>에서 trial version 시스템에 대하여 라이센스 키 신청할 수 있습니다.

NOTE : T-code : SLICENSE에서 링크로 접근 가능한 URL으로 접근 말고, 위 링크 통해 접근하시면 됩니다.

a) NPL – SAP NetWeaver 7.x (Sybase ASE) 을 선택

![image39]

b) 개인정보를 입력하시고, 라이센스 동의 내용을 확인 후 수락

c) 우측 하단의 Generate 버튼을 통해 진행

d) 이후 요청한 system/key에 대하여 .txt 파일이 자동적으로 생성되고, 이를 다운로드 하시면 됩니다.

4. T-code : SLICENSE를 실행하여 라이센스 키를 설치하기

a) Digitally signed Licenses 탭에서 기존 라이센스를 삭제한 다음 Install을 선택합니다. 이후, 다운로드 받은 텍스트 파일을 열고 새 라이센스 키가 설치하세요.

모두 완료되면 시스템 유형이 데모로 변경됩니다. 이제 이클립스의 ABAP 툴(ADT 등)과 CDS 파일 뷰 또는 SAPUI5 UI와 같은 새로운 기능을 사용하여 데모 시나리오를 살펴보고 개발해볼 수 있습니다.

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