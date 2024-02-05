# Inventory of devices on network

### Host Discovery
``` Bash
nmap -sn -n #IP RANGE#
```
### OS Fingerprinting
```bash 
nmap -sT -p22,89 -sV #IP RANGE# 
```

# Baseline network devices

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

# Basic System Info

## Distro Info
```bash
lsb_release -a
```
```Output```
```Bash
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy
```
## Kernel Info
```Bash
uname -a
```
```Output```
```bash
Linux Ichiraku 5.15.133.1-microsoft-standard-WSL2 #1 SMP Thu Oct 5 21:02:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```
## View kernel config
```Bash
cat /proc/sys/kernel/#FILE NAME#
```
```Output varies based which file selected in /proc/sys/kernel#```

## Linux File System

### Find Mount
```Bash
findmnt
```
### Check Mount
```Bash
mount | grep #Directory#
```
### check if mount point
```Bash
mountpoint #Directory#
```
### Check if NFS Server
```Bash
cat /etc/exports
exportfs
```
### Check RPC
```Bash
rpinfo -p
```
## Patches/Updates

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
```Bash 
systemctl -a 

#Output list has been trimmed#
#  UNIT                                                                                                                                         >
#   proc-sys-fs-binfmt_misc.automount                                                                                                            >
#   dev-disk-by\x2did-scsi\x2d3600224801682b0e2be5c8033774f59ba.device                                                                           >
#   dev-disk-by\x2did-scsi\x2d360022480aa6caf3fcdcc249918eed709.device                                                                           >
#   dev-disk-by\x2did-scsi\x2d360022480c9dc3ceb171261d2e3751e69.device                                                                           >
#   dev-disk-by\x2did-wwn\x2d0x600224801682b0e2be5c8033774f59ba.device                                                                           >
#   dev-disk-by\x2did-wwn\x2d0x60022480aa6caf3fcdcc249918eed709.device                                                                           >
#   dev-disk-by\x2did-wwn\x2d0x60022480c9dc3ceb171261d2e3751e69.device
```

### List Configured Services
```Bash
systemctl list-units

#Output list has been trimmed#
#   UNIT                                                                                                                                         >
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-9961b7e7\x2d69ce\x2d41c3\x2d9464\x2ddc910d85059a-net-eth0.device                    >
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-b5b95c49\x2d27f2\x2d4a7a\x2d87ec\x2defa3c1e4ae9a-pci27f2:00-27f2:00:00.0-virtio0-vir>
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-b5b95c49\x2d27f2\x2d4a7a\x2d87ec\x2defa3c1e4ae9a-pci27f2:00-27f2:00:00.0-virtio0-vir>
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-fd1d2cbd\x2dce7c\x2d535c\x2d966b\x2deb5f811c95f0-host0-target0:0:0-0:0:0:0-block-sda>
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-fd1d2cbd\x2dce7c\x2d535c\x2d966b\x2deb5f811c95f0-host0-target0:0:0-0:0:0:1-block-sdb>
#   sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-fd1d2cbd\x2dce7c\x2d535c\x2d966b\x2deb5f811c95f0-host0-target0:0:0-0:0:0:2-block-sdc>
#   sys-devices-platform-serial8250-tty-ttyS0.device                                                                                             >
#   sys-devices-platform-serial8250-tty-ttyS1.device                                                                                             >
#   sys-devices-platform-serial8250-tty-ttyS2.device                                                                                             >
#   sys-devices-platform-serial8250-tty-ttyS3.device                                                                                             >
#   sys-devices-virtual-block-ram0.device
```

### Start Service
```Bash
systemctl start <service name>
```

### Enable Service
```Bash
systemctl enable <service name>
```

### List Network Services

```Bash
netstat -antp | grep LISTEN

#Output#
# tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      133/systemd-resolve

lsof -i -n | grep LISTEN

```