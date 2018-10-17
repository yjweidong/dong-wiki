# Automation Infrastructure Space

This section focus on automation infrastructure setup

## VMWare setup
tips

## Jenkins setup
Automation Infrastructure Setup

## Client Setup 
### Windows Testbed setup:
  * [Disable windows firewall and defender](https://www.windowscentral.com/how-permanently-disable-windows-defender-windows-10)
  * [Disable Automatic Windows Update](http://www.thewindowsclub.com/turn-off-windows-update-in-windows-10)
  * [Disable windows activation pop up if necessary](http://www.thewindowsclub.com/disable-auto-activation-feature-windows-7-8)
  * Disabling sleep:
    * select *Power & Sleep settings*
    * For the drop down menu under *When plugged in, turn off after*, select never
	* For the drop down menu under *When plugged in, PC goes to sleep after*, select never
  * Disable Windows User Account Controls:
    * select *User Account Control* in the start bar
	* drag the notification scroll down to "Never notify" on the bottom
  * Disable Windows SmartScreen Feature (Windows 8 and above only)
    * Search *SmartScreen* in the start bar and click *Change SmartScreen settings*
	* Click the arrow beside *Security*, then click *Change settings* under *Windows SmartScreen*
  * Install Python 2.7.x 32 bit and check option to add python path to environment variables*
  *	Donwload and Install Git client on the client, and then copy Git folder to match our Jenkins setup(E.g. under root directory "c:\") 
  *	Install Java JDK 1.8 (Eg. 8u151)
  *	[Setup Jenkins slave](https://wiki.absolute.com/display/TA/Setting+up+New+VM+on+Jenkins)
  *	If remote ssh is needed, install OpenSSH if it's client and a test agent is associated with it.
  * If automatic login for the user is needed, [Enable automatic logon](https://support.microsoft.com/en-ca/help/324737/how-to-turn-on-automatic-logon-in-windows)
    * Locate the following subkey in the registry *HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon*
		Add *DefaultUserName* string entry, type your user name, and then click OK
		Add *DefaultPassword* string entry, type your password, and then click OK
		If you have joined the computer to a domain, add the *DefaultDomain* string value
		Edit *AutoAdminLogon* entry, type 1 and then click OK

### Mac Testbed setup:	
  *	Disable Automatically check for updates via System Preference → App Store
  *	Disable sudo password popup
	Open terminal, then sudo visudo, change this line:

	$ %admin ALL=(ALL) ALL

	TO:

	$ %admin ALL=(ALL) NOPASSWD: ALL

  *	Install Java 8 or above
  *	Install Git and match our Jenkins setup
  *	Install Python (Make sure the PATH is the correct one, i.e. the default one that Jenkin uses)
  *	Install Pip
  *	Install Pytest (and related item such as pytest-html)
  *	Enable remote management and login
  *	If necessary, enable automatic login for the user

### Install OpenSSH on Windows Client (Optional):
  *	[Install OpenSSH](https://winscp.net/eng/docs/guide_windows_openssh_server#installing_sftp_ssh_server)
    * Download the latest OpenSSH for [Windows binaries](https://github.com/PowerShell/Win32-OpenSSH/releases) including package OpenSSH-Win64.zip or OpenSSH-Win32.zip
    * As the Administrator, extract the package to C:\Program Files\OpenSSH
	* As the Administrator, install sshd and ssh-agent services: 
		powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1
	* Set sshd and ssh-agent services as automatic start and Log On as Local System account, then start
	* Start a SSH client (such as Mobaxterm) to make a SSH connection


