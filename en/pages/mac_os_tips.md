# Mac OS Technologies and Tips Space


## Mac OS 
  * [Daemons and Agents Technical Notes](https://developer.apple.com/library/archive/technotes/tn2083/_index.html#//apple_ref/doc/uid/DTS10003794-CH1-SECTION23)


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

	for Mac 10.14 SSH session may be constantly disconnected after minutes. Need to make SSH server keep connection alive via https://stackoverflow.com/questions/8660532/avoiding-ssh-timeouts-on-mac-os
	  In general, create the following settings in the config file .ssh/config:
		Host *
		 ServerAliveInterval 60
	For benchmark test, need to install:
		Install telegraf via "brew install telegraf". See https://docs.influxdata.com/telegraf/v1.10/introduction/installation/
		Install matplotlib via "pip install matplotlib" 

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
  
### Performance monitoring tools-installed
  * top 
    * Eg. track process <pid> with sorting key as cpu in logging mode: top -ocpu -s 1 -pid <pid> -stats "pid,command,cpu,mem" -l 0
		bash-3.2# top -ocpu -n50 -s 1 -pid 1635 -l 0 -stats pid,command,cpu,mem
		Processes: 287 total, 2 running, 285 sleeping, 881 threads
		2019/03/12 11:24:35
		Load Avg: 1.37, 1.25, 1.16
		CPU usage: 3.7% user, 9.23% sys, 87.69% idle
		SharedLibs: 344M resident, 63M data, 50M linkedit.
		MemRegions: 24238 total, 1734M resident, 156M private, 533M shared.
		PhysMem: 4858M used (1695M wired), 11G unused.
		VM: 1367G vsize, 1297M framework vsize, 0(0) swapins, 0(0) swapouts.
		Networks: packets: 649298/141M in, 164806/114M out.
		Disks: 91033/1808M read, 148571/2320M written.

		PID   COMMAND %CPU MEM
		1635  hdc     0.0  5820K+

	* Eg. track process <pid> with filter for stats line only in logging mode:  
	    bash-3.2# top -s 1 -pid 1635 -l 0 -stats pid,command,cpu,mem  | awk 'NR%13==0'
		1635  hdc     0.0  5820K+
		1635  hdc     0.0  5820K

	* Get process CPU usage at https://stackoverflow.com/questions/16726779/how-do-i-get-the-total-cpu-usage-of-an-application-from-proc-pid-stat
