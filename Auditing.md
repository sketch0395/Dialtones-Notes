
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
#OS Info#
get-ciminstance win32_operatingsystem
#OS Info#
wmic os list brief
```
### Linux
```bash
#Distro Info#
lsb_release -a
#Kernel Info#
uname -a
#View kernel config
cat /proc/sys/kernel/#FILE NAME#
```
## Disk Drive Info

### Windows
```powershell
#Physical Drive#
get-physicaldisk
wmic diskdrive list brief
#Disk Partition#
Get-partition
#Disk Volume#
get-volume
wmi logicaldisk list
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