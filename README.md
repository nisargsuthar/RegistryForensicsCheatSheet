# Windows Registry Forensics Cheat Sheet

Load the appropriate hives in the software of your choice and follow these conventions for this cheatsheet:\
"" - Indicates the field value to look for.\
'' - Indicates the arbitrary placeholder for identifiers.\
() - Extra relevant information.

Control Set:\
&emsp;System > Select > "Current"

Computer Name:\
&emsp;System > ControlSetXXX > Control > ComputerName > "ComputerName"

Current Timezone:\
&emsp;System > ControlSetXXX > Control > TimeZoneInformation > "TimeZoneKeyName"

System Install Date:\
&emsp;Software > Microsoft > WindowsNT > CurrentVersion > "InstallDate"\
&emsp;<b>NOTE:\- Decode it from Unix format.

Last Logged On User:\
&emsp;Software > Microsoft > Windows > CurrentVersion > Authentication > LogonUI > "LastLoggedOnUser"

Last Shutdown Time:\
&emsp;System > ControlSetXXX > Control > Windows > "ShutdownTime"\
&emsp;<b>NOTE:\- Decode it from Hex format.

Autostart Applications:\
&emsp;NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Run

Searched terms in Windows:\
&emsp;NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > WordWheelQuery

Recently Accessed Files:\
&emsp;NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > RecentDocs

Windows Run Queries:\
&emsp;NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > RunMRU

Relative Identifier for a user:\
&emsp;SAM > Domains > Account > Users > Names > User

User Created Accounts (Look for Relative Identifiers > 1000):\
&emsp;SAM > Domains > Account > Users > Names

Machine Identifier (Last 12 bytes):\
&emsp;SAM > Domains > Account > "V"\
&emsp;<b>NOTE:\- Group into 3 sets of 4, convert to little endian and convert from hex to dec.

USB devices connected:\
&emsp;System > ControlSetXXX > Enum > USBSTOR

Serial Number of USB device mounted:\
&emsp;System > MountedDevices

Network Connections:\
&emsp;Software > Microsoft > Windows NT > CurrentVersion > NetworkList

Install date of applications:\
&emsp;Amcache.hve > {GUID} > InventoryApplication > 'ProgramID' > "InstallDate"

Last executed time of applications:\
&emsp;NTUSER.dat > Software > Microsoft > Windows > CurrentVersion > Explorer > UserAssist> {GUID} (ROT13 encoded)

Pagefile cleared at shutdown? (Used for swapping RAM):\
&emsp;System > ControlSetXXX > Control > Session Manager > Memory Management > "ClearPageFileAtShutdown"\
&emsp;<b>NOTE:\- If value is 0, then look for the pagefile.sys file for the memory capture.
