# Windows Registry Forensics Cheat Sheet

---
Load the appropriate hives in the software of your choice and follow these conventions for this cheatsheet:

```
"" - Indicates the field value to look for.
'' - Indicates the arbitrary placeholder for identifiers.
{} - Indicates the arbitrary placeholder for GUID.
() - Extra relevant information.
```
---

Control Set:\
`System > Select > "Current"`

Computer Name:\
`System > ControlSetXXX > Control > ComputerName > "ComputerName"`

Current Timezone:\
`System > ControlSetXXX > Control > TimeZoneInformation > "TimeZoneKeyName"`

System Install Date:\
`Software > Microsoft > WindowsNT > CurrentVersion > "InstallDate"`\
NOTE:- Decode it from Unix format.

Last Logged On User:\
`Software > Microsoft > Windows > CurrentVersion > Authentication > LogonUI > "LastLoggedOnUser"`

Last Shutdown Time:\
`System > ControlSetXXX > Control > Windows > "ShutdownTime"`\
NOTE:- Decode it from Hex format.

Autostart Applications:\
`NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Run`

Searched terms in Windows:\
`NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > WordWheelQuery`

Recently Accessed Files:\
`NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > RecentDocs`

Windows Run Queries:\
`NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > RunMRU`

Relative Identifier for a user:\
`SAM > Domains > Account > Users > Names > User`

User Created Accounts (Look for Relative Identifiers > 1000):\
`SAM > Domains > Account > Users > Names`

Machine Identifier (Last 12 bytes):\
`SAM > Domains > Account > "V"`\
NOTE:- Group into 3 sets of 4, convert to little endian and convert from hex to dec.

USB devices connected:\
`System > ControlSetXXX > Enum > USBSTOR`

Serial Number of USB device mounted:\
`System > MountedDevices`

Network Connections:\
`Software > Microsoft > Windows NT > CurrentVersion > NetworkList`

Install date of applications:\
`Amcache.hve > {GUID} > InventoryApplication > 'ProgramID' > "InstallDate"`

Last executed time of applications:\
`NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > UserAssist> {GUID} (ROT13 encoded)`

Pagefile cleared at shutdown? (Used for swapping RAM):\
`System > ControlSetXXX > Control > Session Manager > Memory Management > "ClearPageFileAtShutdown"`\
NOTE:- If value is 0, then look for the pagefile.sys file for the memory capture.
