## Window Events

| Type | Event ID | Log Type |
| ------ | ------ | ------| 
| Create Service | 7030, 7045 (system) 4697 (security) | System/security |
| Command Line Audit | 4688 | Security |   
| Create User | 4720, 4722, 4724, 4738 | Security
| Add User to Group | 4728, 4732, 4735, 4737, 4755 | Security | 
| Clear event Log | 1102 | Security 
| Create RDP Cert | 1056 | Security 
| Insert USB | 7045, 10000, 10001, 10100, 20001, 20003, 24576, 24577, 24579 | Security 
| Disable Firewall | 2003, 2005 | Firewall
| Applocker | 8003, 8004, 8006, 8007 | Applocker | 


```Powershell
get-winevent @{LogName="Log Type"; id="Event ID"}
```

```OUTPUT: Example of Log type "Security" ID "4720" (Create User)```

```Powerhsell

   ProviderName: Microsoft-Windows-Security-Auditing

TimeCreated                      Id LevelDisplayName Message
-----------                      -- ---------------- -------
2/5/2024 8:45:18 AM            4720 Information      A user account was created....
2/5/2024 7:58:37 AM            4720 Information      A user account was created....
2/5/2024 5:54:54 AM            4720 Information      A user account was created....
2/3/2024 11:25:09 PM           4720 Information      A user account was created....
2/2/2024 11:20:54 PM           4720 Information      A user account was created....
2/2/2024 11:02:35 PM           4720 Information      A user account was created....
2/2/2024 11:02:34 PM           4720 Information      A user account was created....
2/2/2024 11:47:59 PM           4720 Information      A user account was created....
```