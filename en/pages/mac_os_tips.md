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

### Install Git on Mac
	http://modulesunraveled.com/installing-git/installing-git-if-you-do-not-have-xcode-or-command-line-developer-tools-installed
	
### Install HTTP server:
	[Notes](https://discussions.apple.com/docs/DOC-3083)
	Default document location is /Library/WebServer/Documents/ defined in /etc/apache2/httpd.conf
	To check http configuration, run: apachectl configtest
	To launch http daemon, run: sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist
	
## Codesign:
	Check code sign: codesign -dvvvv <file>
	Remove code sign: codesign --remove-signature <file>	
	
	
## Tips

  * [Prevent 'grep' from showing up in ps results](https://unix.stackexchange.com/questions/74185/how-can-i-prevent-grep-from-showing-up-in-ps-results)
    * pgrep for display PID of a process, or execute ps -ax | grep "[h]dc"
  *
  
### Tools:
  * [online tool to decode/encode with hash] (https://emn178.github.io/online-tools/)

