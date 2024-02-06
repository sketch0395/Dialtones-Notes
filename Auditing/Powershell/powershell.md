## Basic System Info

```Powershell
$PSVersionTable
```
```OUTPUT:Windows Powershell | Powershell.exe version 5.1```
```Powershell
Name                           Value
----                           -----
PSVersion                      5.1.20348.558
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.20348.558
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

```OUTPUT:Powershell Core | PWSH.exe version 7 and up```
```Powershell
Name                           Value
----                           -----
PSVersion                      7.4.1
PSEdition                      Core
GitCommitId                    7.4.1
OS                             Microsoft Windows 10.0.22631
Platform                       Win32NT
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0…}
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
WSManStackVersion              3.0
```

## Alias Information

```Powershell
Get-Alias
```
```OUTPUT:Windows Powershell```
```Powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility
Alias           chdir -> Set-Location
```

```OUTPUT:Windows Powershell Core```
```Powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           ? -> Where-Object
Alias           % -> ForEach-Object
Alias           ac -> Add-Content
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           chdir -> Set-Location
Alias           clc -> Clear-Content
Alias           clear -> Clear-Host
Alias           clhy -> Clear-History
Alias           cli -> Clear-Item
Alias           clp -> Clear-ItemProperty
```

## Help
```Powershell
Get-Help
#or
(Command) -?
```
## Basic information
```Powershell
systeminfo
```

```Output```
```Powershell
System Model:              
System Type:               
Processor(s):              
BIOS Version:             
Windows Directory:         
System Directory:          
Boot Device:               
System Locale:             
Input Locale:              
Time Zone:                 
Total Physical Memory:     
Available Physical Memory: 
Virtual Memory: Max Size:  
Virtual Memory: Available: 
Virtual Memory: In Use:    
Page File Location(s):     
Domain:                    
Logon Server:              
Hotfix(s):                 
Network Card(s): 
```
## OS Info
```Powershell
get-ciminstance win32_operatingsystem
```
```Output```
```Powershell
SystemDirectory     Organization BuildNumber RegisteredUser                SerialNumber            Version
---------------     ------------ ----------- --------------                ------------            -------
```Powershell
wmic os list brief
```
```Output```
```Powershell
BuildNumber  Organization  RegisteredUser                 SerialNumber             SystemDirectory      Version
```

## Disk Drive Info

```powershell
#Physical Drive#
get-physicaldisk

#or

wmic diskdrive list brief
```
```Output```
```Powershell
Number FriendlyName              SerialNumber    MediaType CanPool OperationalStatus HealthStatus Usage            Size
------ ------------              ------------    --------- ------- ----------------- ------------ -----            ----
0      WDC WD10SPZX-60Z10T0      WD-WX61AB98X224 HDD       False   OK                Healthy      Auto-Select 931.51 GB
1      SanDisk SD6SN1M-256G-1006 143283402698    SSD       False   OK                Healthy      Auto-Select 238.47 GB

#or

Caption                    DeviceID            Model                      Partitions  Size
WDC WD10SPZX-60Z10T0       \\.\PHYSICALDRIVE0  WDC WD10SPZX-60Z10T0       1           1000202273280
SanDisk SD6SN1M-256G-1006  \\.\PHYSICALDRIVE1  SanDisk SD6SN1M-256G-1006  3           256052966400
```
## Disk Partition
```Powershell
Get-partition
```
```Output```
```Powershell
   DiskPath: \\?\scsi#disk&ven_sandisk&prod_sd6sn1m-256g-100#5&2075d53c&0&010000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                                          Size Type
---------------  ----------- ------                                                          ---- ----
1                           1048576                                                       260 MB System
2                           273678336                                                      16 MB Reserved
3                C           290455552                                                  237.63 GB Basic
4                           255442550784                                                  584 MB Recovery

   DiskPath: \\?\scsi#disk&ven_wdc&prod_wd10spzx-60z10t0#5&2075d53c&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                                          Size Type
---------------  ----------- ------                                                          ---- ----
1                D           1048576                                                    931.51 GB Basic
```
## Disk Volume
```Powershell
get-volume

#or

wmi logicaldisk list | Out-Gridview 
#Presents better when able to view as grid
```
```Output```
```Powershell
DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
D           DATA         NTFS           Fixed     Healthy      OK                    595.13 GB 931.51 GB
C           WINDOWS      NTFS           Fixed     Healthy      OK                    136.65 GB 237.63 GB
            SYSTEM       FAT32          Fixed     Healthy      OK                    173.92 MB    256 MB
                         NTFS           Fixed     Healthy      OK                     48.64 MB    584 MB

#or 

Access  Availability  BlockSize  Caption  Compressed  ConfigManagerErrorCode  ConfigManagerUserConfig  Description       DeviceID  DriveType  ErrorCleared  ErrorDescription  ErrorMethodology  FileSystem  FreeSpace     InstallDate  LastErrorCode  MaximumComponentLength  MediaType  Name  NumberOfBlocks  PNPDeviceID  PowerManagementCapabilities  PowerManagementSupported  ProviderName  Purpose  QuotasDisabled  QuotasIncomplete  QuotasRebuilding  Size           Status  StatusInfo  SupportsDiskQuotas  SupportsFileBasedCompression  VolumeName  VolumeSerialNumber
0                                C:       FALSE                                                        Local Fixed Disk  C:        3
                                    NTFS        146729218048                              255                     12         C:
                                                                                  TRUE            TRUE              FALSE             255151251456
             TRUE                TRUE                          WINDOWS     04F40E25
0                                D:       FALSE                                                        Local Fixed Disk  D:        3
                                    NTFS        639013515264                              255                     12         D:
                                                                                  TRUE            FALSE             FALSE             1000203087872
             TRUE                TRUE                          DATA        123C535C
```

### File Share
```powershell
#List SMB shares#
get-smbshare
#List File Share#
get-fileshare
```
## Patches/Updates
### Windows
```Powershell
#Installed Patches#
get-hotfix
wmic qfe list brief
#Installed Apps#
get-wmiobject win32_product
wmic product list brief
```

# Network / Local Services

### List Services
``` powershell 
get-service

#or

wmic service list brief
```
```Output``` example list has been trimmed

```Powershell
Status   Name               DisplayName
------   ----               -----------
Stopped  AarSvc_dcb5d       Agent Activation Runtime_dcb5d
Running  AdobeARMservice    Adobe Acrobat Update Service
Stopped  AJRouter           AllJoyn Router Service
Stopped  ALG                Application Layer Gateway Service
Running  AMD Crash Defende… AMD Crash Defender Service
Running  AMD External Even… AMD External Events Utility
Running  AppIDSvc           Application Identity

#or

Output example list has be trimmed#
ExitCode  Name                                      ProcessId  StartMode  State    Status
0         AdobeARMservice                           6088       Auto       Running  OK
1077      AJRouter                                  0          Manual     Stopped  OK
1077      ALG                                       0          Manual     Stopped  OK
0         AMD Crash Defender Service                4500       Auto       Running  OK
0         AMD External Events Utility               4492       Auto       Running  OK
0         AppIDSvc                                  868        Manual     Running  OK
0         Appinfo                                   10048      Manual     Running  OK
1077      AppMgmt                                   0          Manual     Stopped  OK
```
## List Process
```Powershell
ps
```
```Output``` example list has been trimmed
```Powershell
#  NPM(K)    PM(M)      WS(M)     CPU(s)      Id  SI ProcessName
#  ------    -----      -----     ------      --  -- -----------
#      19     6.31       8.16      55.81    9600   1 AdobeCollabSync
#      14     3.91       4.37       1.17   10660   1 AdobeCollabSync
#      11     2.78      10.79       0.30    8064   0 AggregatorHost
#       9     2.22       7.42       0.00    4500   0 amdfendrsr
#      18     5.25      16.73       4.25    2788   0 AppHelperCap
#      19     5.05      24.98       0.14    6644   1 ApplicationFrameHost
#       9     1.80       8.57       0.00   24120   1 AppVShNotify
#      10     1.97       7.25       0.08    6088   0 armsvc
#      16     3.84      14.31      14.80    4752   1 atieclxx
#       9     1.64       6.64       0.05    4492   0 atiesrxx
```
### List Running Process
```Powershell
tasklist

#or

wmic process list brief
```

```Output``` list has been trimmed#
```Powershell
Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0      4,044 K
Secure System                  108 Services                   0     40,708 K
Registry                       156 Services                   0     37,020 K
smss.exe                       588 Services                   0      1,284 K
csrss.exe                     1072 Services                   0      5,468 K
wininit.exe                   1196 Services                   0      6,596 K

or

HandleCount  Name                                                           Priority  ProcessId  ThreadCount  WorkingSetSize
0            System Idle Process                                            0         0          16           8192
6845         System                                                         8         4          296          4145152
0            Secure System                                                  8         108        0            41684992
0            Registry                                                       8         156        4            37871616
58           smss.exe                                                       11        588        2            1314816
829          csrss.exe                                                      13        1072       13           5595136
145          wininit.exe                                                    13        1196       2            6754304
981          csrss.exe                                                      13        1216       16           14962688
281          winlogon.exe                                                   13        1308       3            11599872
889          services.exe                                                   9         1328       7            17014784
```