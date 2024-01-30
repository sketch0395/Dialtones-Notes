
## Inventory

### Host Discovery
``` Bash
nmap -sn -n #IP RANGE#
```
### OS Fingerprinting
```bash 
nmap -sT -p22,89 -sV #IP RANGE# 
```

## Baseline

### Create Baseline
```bash
nmap -sT -p 1-65535 #IP RANGE# -oX Baseline.xml
```
### Create Observed
```bash
nmap -sT -p 1-65535 #IP RANGE# -oX Observed.xml
```
### Compare Files
``` bash
yandiff --Baseline.xml --Observed.xml
```
## Basic System Info

### Windows
          
```Powershell
#Basic information#
systeminfo
#Output#
# System Model:              
# System Type:               
# Processor(s):              
# BIOS Version:             
# Windows Directory:         
# System Directory:          
# Boot Device:               
# System Locale:             
# Input Locale:              
# Time Zone:                 
# Total Physical Memory:     
# Available Physical Memory: 
# Virtual Memory: Max Size:  
# Virtual Memory: Available: 
# Virtual Memory: In Use:    
# Page File Location(s):     
# Domain:                    
# Logon Server:              
# Hotfix(s):                 
# Network Card(s): 

#OS Info#
get-ciminstance win32_operatingsystem
#Output#
# SystemDirectory     Organization BuildNumber RegisteredUser                SerialNumber            Version
# ---------------     ------------ ----------- --------------                ------------            -------

#OS Info#
wmic os list brief
#Output#
# BuildNumber  Organization  RegisteredUser                 SerialNumber             SystemDirectory      Version
```
### Linux
```bash
#Distro Info#
lsb_release -a
#Output#
#<
#No LSB modules are available.
#Distributor ID: Ubuntu
#Description:    Ubuntu 22.04.3 LTS
#Release:        22.04
#Codename:       jammy

#Kernel Info#
uname -a
#Output#
#Linux Ichiraku 5.15.133.1-microsoft-standard-WSL2 #1 SMP Thu Oct 5 21:02:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux#

#View kernel config
cat /proc/sys/kernel/#FILE NAME#
#Output varies based which file selected in /proc/sys/kernel#

```
## Disk Drive Info

### Windows
```powershell
#Physical Drive#
get-physicaldisk
#Output
#Number FriendlyName              SerialNumber    MediaType CanPool OperationalStatus HealthStatus Usage            Size
# ------ ------------              ------------    --------- ------- ----------------- ------------ -----            ----
# 0      WDC WD10SPZX-60Z10T0      WD-WX61AB98X224 HDD       False   OK                Healthy      Auto-Select 931.51 GB
# 1      SanDisk SD6SN1M-256G-1006 143283402698    SSD       False   OK                Healthy      Auto-Select 238.47 GB
wmic diskdrive list brief
#Caption                    DeviceID            Model                      Partitions  Size
# WDC WD10SPZX-60Z10T0       \\.\PHYSICALDRIVE0  WDC WD10SPZX-60Z10T0       1           1000202273280
# SanDisk SD6SN1M-256G-1006  \\.\PHYSICALDRIVE1  SanDisk SD6SN1M-256G-1006  3           256052966400
#Disk Partition#
Get-partition
#Output
#    DiskPath: \\?\scsi#disk&ven_sandisk&prod_sd6sn1m-256g-100#5&2075d53c&0&010000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

# PartitionNumber  DriveLetter Offset                                                          Size Type
# ---------------  ----------- ------                                                          ---- ----
# 1                           1048576                                                       260 MB System
# 2                           273678336                                                      16 MB Reserved
# 3                C           290455552                                                  237.63 GB Basic
# 4                           255442550784                                                  584 MB Recovery

#    DiskPath: \\?\scsi#disk&ven_wdc&prod_wd10spzx-60z10t0#5&2075d53c&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

# PartitionNumber  DriveLetter Offset                                                          Size Type
# ---------------  ----------- ------                                                          ---- ----
# 1                D           1048576                                                    931.51 GB Basic
#Disk Volume#
get-volume
#Output
# DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
# ----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
# D           DATA         NTFS           Fixed     Healthy      OK                    595.13 GB 931.51 GB
# C           WINDOWS      NTFS           Fixed     Healthy      OK                    136.65 GB 237.63 GB
#             SYSTEM       FAT32          Fixed     Healthy      OK                    173.92 MB    256 MB
#                          NTFS           Fixed     Healthy      OK                     48.64 MB    584 MB
wmi logicaldisk list | Out-Gridview 
#Presents better when able to view as grid
#Output
# Access  Availability  BlockSize  Caption  Compressed  ConfigManagerErrorCode  ConfigManagerUserConfig  Description       DeviceID  DriveType  ErrorCleared  ErrorDescription  ErrorMethodology  FileSystem  FreeSpace     InstallDate  LastErrorCode  MaximumComponentLength  MediaType  Name  NumberOfBlocks  PNPDeviceID  PowerManagementCapabilities  PowerManagementSupported  ProviderName  Purpose  QuotasDisabled  QuotasIncomplete  QuotasRebuilding  Size           Status  StatusInfo  SupportsDiskQuotas  SupportsFileBasedCompression  VolumeName  VolumeSerialNumber
# 0                                C:       FALSE                                                        Local Fixed Disk  C:        3
#                                     NTFS        146729218048                              255                     12         C:
#                                                                                   TRUE            TRUE              FALSE             255151251456
#              TRUE                TRUE                          WINDOWS     04F40E25
# 0                                D:       FALSE                                                        Local Fixed Disk  D:        3
#                                     NTFS        639013515264                              255                     12         D:
#                                                                                   TRUE            FALSE             FALSE             1000203087872
#              TRUE                TRUE                          DATA        123C535C
```
### Linux File System
```Bash
#Find Mount#
findmnt
#Check Mount#
mount | grep #Directory#
#check if mount point#
mountpoint #Directory#
#Check if NFS Server#
cat /etc/exports
exportfs
#Check RPC#
////////////////
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
### Linux
```bash
#App armored enabled#
sudo aa-status
#Upgradable Packages#
sudo apt update
#Patch History#
cat /var/log/dpkg.log #or# 
cat /var/log/dnf.rpm.log
#Patch Date#
sudo awk '/installed/{print $1}' /var/log/dpkg.log | sort | uniq -c
```

## Network / Local Services

### List Services
``` powershell 
get-service
wmic service list brief
```