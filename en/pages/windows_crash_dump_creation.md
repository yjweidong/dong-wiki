# Automation Space


Prerequisites
Install Debugging Tools for Windows (see References section for link)
<Path to windbg.exe> in the below sections means Path to windbg.exe present in the debugging tools installed as part of previous step. If debugging tools are installed using Windows 10 SDK (works on Windows 7 as well), the common installation path is C:\Program Files (x86)\Windows Kits\10\Debuggers\x64 for 64-bit Windbg and C:\Program Files (x86)\Windows Kits\10\Debuggers\x86 for 32-bit Windbg.
<Path to dumps folder> in the below sections means Path where application memory dumps would get stored. This path needs to be created beforehand and the folder should be writable without requiring any UAC elevation. An example of a valid path would be C:\dumps folder.
Extract attached 
CrashTest.zip
 CrashTest.zip file to a folder. This contains 2 exe files CrashTest_x86.exe (32-bit) and CrashTest_x64.exe (64-bit). Both of these would crash (divide by zero) on execution.
Generating application crash dump automatically on application crash
For 32-bit binaries on 32-bit machines and 64-bit binaries on 64-bit machines
Launch regedit and navigate to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug
Create following 2 values (if not existing already):
Value name: Auto
Value type: REG_SZ
Value data: 1
Value name: Debugger
Value type: REG_SZ
Value data: "<Path to windbg.exe>" -p %ld -c ".dump /ma /u <Path to dumps folder>\crash.dmp;.logopen /t <Path to dumps folder>\crash.txt;.symfix;!analyze -v;.logclose;q" -e %ld –g
Launch CrashTest_x86.exe to verify if dump and analysis file gets generated in the dumps folder for 32-bit processes. Launch CrashTest_x64.exe to verify if dump and analysis file gets generated in the dumps folder for 64-bit processes.
 For 32-bit binaries on 64-bit machines:
Launch regedit and navigate to HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
Create following 2 values (if not existing already):
Value name: Auto
Value type: REG_SZ
Value data: 1
Value name: Debugger
Value type: REG_SZ
Value data: "<Path to windbg.exe>" -p %ld -c ".dump /ma /u <Path to dumps folder>\crash.dmp;.logopen /t <Path to dumps folder>\crash.txt;.effmach x86 ;.symfix;!analyze -v;.logclose;q" -e %ld –g
Launch CrashTest_x86.exe to verify if dump and analysis file gets generated in the dumps folder.


Generating Complete memory dump automatically on a Blue screen
Launch regedit and navigate to HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
Create following value:
Value name: CrashDumpEnabled
Value type: REG_DWORD
Value data: 0x1
Ensure System Page file size is at least set to Size of Physical memory + 1 MB


Forcing System crash from keyboard in the event of a System hang
If you have Scroll lock key on your keyboard
For USB keyboards, launch regedit and navigate to HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\kbdhid\Parameters
For PS/2 keyboards (do we still have PS/2 keyboards?), launch regedit and navigate to HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt\Parameters
Create following value:
Value name: CrashOnCtrlScroll
Value type: REG_DWORD
Value data: 0x1
Restart the System
To test, on your keyboard, hold down the rightmost CTRL key, and press the SCROLL LOCK key twice.
Note: This step will lead to Blue screen if the key combination is setup correctly
If system crashed in previous step, on next system start, verify if C:\Windows\MEMORY.dmp file exists. Also verify the dump file timestamp should be time of crash, and dump file size should be equal to amount of physical RAM installed on the system.
For keyboards which don’t have Scroll lock key(like a Laptop keyboard)
The laptop keyboards are mostly connected via USB bus internally. For such cases, we need to define a different key combination to generate System crash which does not include Scroll lock. Following steps will lead to mapping CTRL + ESC + ESC keyboard sequence for generating system crash:

For USB keyboards, launch regedit and navigate to HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\kbdhid

For PS/2 keyboards (if USB did not work for Laptop keyboards), launch regedit and navigate to HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt

Create subkey named crashdump
Create following values under crashdump subkey:
Value name: Dump1Keys
Value type: REG_DWORD
Value data: 0x2
Value name: Dump2Key
Value type: REG_DWORD
Value data: 0x6E
Restart the System
To test, on your keyboard, hold down the rightmost CTRL key, and press the ESC key twice.
Note: This step will lead to Blue screen if the key combination is setup correctly
If system crashed in previous step, on next system start, verify if C:\Windows\MEMORY.dmp file exists. Also verify the dump file timestamp should be time of crash, and dump file size should be equal to amount of physical RAM installed on the system.


References


Debugging Tools for Windows (WinDbg, KD, CDB, NTSD)
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/

Forcing a System Crash from the Keyboard
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/forcing-a-system-crash-from-the-keyboard

How to generate a kernel or a complete memory dump file in Windows Server
https://support.microsoft.com/en-ca/help/969028/how-to-generate-a-kernel-or-a-complete-memory-dump-file-in-windows-ser