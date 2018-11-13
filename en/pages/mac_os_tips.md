# Mac OS Technologies and Tips Space


## Mac OS 
  * [Daemons and Agents Technical Notes](https://developer.apple.com/library/archive/technotes/tn2083/_index.html#//apple_ref/doc/uid/DTS10003794-CH1-SECTION23)


### Mac Testbed setup:
	Configure static IP address to any physical Mac box. See IP allocation above 
	Disable Automatically check for updates via System Preference → App Store
	Create an administration account with user ID as "qa" and well known password.
	Disable sudo password popup

### Install OpenSSH on Windows Client (Optional):
	Some test cases, such as Device freeze, need to be executed remotely since the device will become frozen after applying DFZ request or be forced to reboot after unfreeze.
	Refer to https://winscp.net/eng/docs/guide_windows_openssh_server#installing_sftp_ssh_server for OpenSSH setup.
	Set and start sshd and ssh-agent services: Start type as automatic start and Log On as Local System account
	Start a SSH client (such as Mobaxterm) to run the test

## Tips

  * [TBD](https://developer.apple.com/library/archive/technotes/tn2083/_index.html#//apple_ref/doc/uid/DTS10003794-CH1-SECTION23)

