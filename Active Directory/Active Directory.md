## Forest Information
```Powershell
Get-ASForest -id (domanin name)
```
```OUTPUT```
```
#output#
# ApplicationPartitions : {DC=ForestDnsZones,DC=ramen,DC=test, DC=DomainDnsZones,DC=ramen,DC=test}
# CrossForestReferences : {}
# DomainNamingMaster    : Ramen.ramen.test
# Domains               : {ramen.test}
# ForestMode            : Windows2016Forest
# GlobalCatalogs        : {Ramen.ramen.test}
# Name                  : ramen.test
# PartitionsContainer   : CN=Partitions,CN=Configuration,DC=ramen,DC=test
# RootDomain            : ramen.test
# SchemaMaster          : Ramen.ramen.test
# Sites                 : {Default-First-Site-Name}
# SPNSuffixes           : {}
# UPNSuffixes           : {}
```

## Domain Info

```Powershell
Get-ADDomain -id (domain name)
```
```OUTPUT```
```Powershell

AllowedDNSSuffixes                 : {}
ChildDomains                       : {}
ComputersContainer                 : CN=Computers,DC=ramen,DC=test
DeletedObjectsContainer            : CN=Deleted Objects,DC=ramen,DC=test
DistinguishedName                  : DC=ramen,DC=test
DNSRoot                            : ramen.test
DomainControllersContainer         : OU=Domain Controllers,DC=ramen,DC=test
DomainMode                         : Windows2016Domain
DomainSID                          : S-1-5-21-3130215642-2177870988-1324888700
ForeignSecurityPrincipalsContainer : CN=ForeignSecurityPrincipals,DC=ramen,DC=test
Forest                             : ramen.test
InfrastructureMaster               : Ramen.ramen.test
LastLogonReplicationInterval       :
LinkedGroupPolicyObjects           : {CN={31B2F340-016D-11D2-945F-00C04FB984F9},CN=Policies,CN=System,DC=ramen,DC=test}
LostAndFoundContainer              : CN=LostAndFound,DC=ramen,DC=test
ManagedBy                          :
Name                               : ramen
NetBIOSName                        : RAMENN
ObjectClass                        : domainDNS
ObjectGUID                         : 3aba5141-3d1e-47f3-b0f5-cb2b2b6a1029
ParentDomain                       :
PDCEmulator                        : Ramen.ramen.test
PublicKeyRequiredPasswordRolling   : False
QuotasContainer                    : CN=NTDS Quotas,DC=ramen,DC=test
ReadOnlyReplicaDirectoryServers    : {}
ReplicaDirectoryServers            : {Ramen.ramen.test}
RIDMaster                          : Ramen.ramen.test
SubordinateReferences              : {DC=ForestDnsZones,DC=ramen,DC=test, DC=DomainDnsZones,DC=ramen,DC=test,
                                     CN=Configuration,DC=ramen,DC=test}
SystemsContainer                   : CN=System,DC=ramen,DC=test
UsersContainer                     : CN=Users,DC=ramen,DC=test

```