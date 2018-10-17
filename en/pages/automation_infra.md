# Automation Infrastructure Space

This section focus on automation infrastructure setup

## VMWare setup
tips

## Jenkins setup
Automation Infrastructure Setup

## Client Setup 
### Windows Testbed setup:
  * [Disable windows firewall and defender](https://www.windowscentral.com/how-permanently-disable-windows-defender-windows-10)
  * [Disable windows update](http://www.thewindowsclub.com/turn-off-windows-update-in-windows-10)
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

### Mac Testbed setup:
	Configure static IP address to any physical Mac box. See IP allocation above 
	Disable Automatically check for updates via System Preference → App Store
	Create an administration account with user ID as "qa" and well known password.
	Disable sudo password popup

	Open terminal, then sudo visudo, change this line:

	$ %admin ALL=(ALL) ALL

	TO:

	$ %admin ALL=(ALL) NOPASSWD: ALL

	Install Java 8 or above
	Install Git
	Install Python (Make sure the PATH is the correct one, i.e. the default one that Jenkin uses)
	Install Pip
	Install Pytest (and related item such as pytest-html)
	Enable remote management and login
	Enable automatic login for the user

### Install OpenSSH on Windows Client (Optional):
	Some test cases, such as Device freeze, need to be executed remotely since the device will become frozen after applying DFZ request or be forced to reboot after unfreeze.
	Refer to https://winscp.net/eng/docs/guide_windows_openssh_server#installing_sftp_ssh_server for OpenSSH setup.
	Set and start sshd and ssh-agent services: Start type as automatic start and Log On as Local System account
	Start a SSH client (such as Mobaxterm) to run the test

## Section 2

Automation tips
