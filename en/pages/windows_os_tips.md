# Automation Space


## Infrastructure

Automation Infrastructure Setup

### VMWare setup
tips

### Jenkins setup
Automation Infrastructure Setup

### Performance testing:
	https://medium.com/the-telegraph-engineering/performance-testing-using-gatling-tool-b3adeeaefb77

### Registry:
	On windows 64bit OS, registry key will be created under "HKLM\Software" for 64bit application, and under "HKLM\Software\WOW6432Node" for 32bit application
	See different logical view at https://docs.microsoft.com/en-us/windows/desktop/WinProg64/registry-redirector

### Windows Testbed setup:
	Refer to https://wiki.absolute.com/pages/viewpage.action?pageId=13369722 for VM setup. 
	Disable windows firewall and defender (https://www.windowscentral.com/how-permanently-disable-windows-defender-windows-10)
	Disable windows update (http://www.thewindowsclub.com/turn-off-windows-update-in-windows-10)
	Disable windows activation pop up if necessary http://www.thewindowsclub.com/disable-auto-activation-feature-windows-7-8
	Install Python 2.7.x 32 bit and check option to add python path to environment variables*
	Install Git client on the VM and copy Git folder under root directory "c:\" to match our Jenkins setup 
	Install Java JDK 1.8 (Eg. 8u151) to the VM
	Setup Jenkins slave via https://wiki.absolute.com/display/TA/Setting+up+New+VM+on+Jenkins
	If remote ssh is needed, install OpenSSH if it's client and a test agent is associated with it.
	After cloning the python script from Git, run the script to install pytest "python setup.py -c dfz -pytest"

### Install OpenSSH on Windows Client (Optional):
	Some test cases, such as Device freeze, need to be executed remotely since the device will become frozen after applying DFZ request or be forced to reboot after unfreeze.
	Refer to https://winscp.net/eng/docs/guide_windows_openssh_server#installing_sftp_ssh_server for OpenSSH setup.
	Set and start sshd and ssh-agent services: Start type as automatic start and Log On as Local System account
	Start a SSH client (such as Mobaxterm) to run the test

## Section 2

Automation tips

### Pycharm and Python:
	1) resolve "unresolved reference issue in Pycharm": Add parent folder (source roots) to Pycharm PYTHONPATH (right click the folder then Mark Directory As "Source Root")
		https://stackoverflow.com/questions/21236824/unresolved-reference-issue-in-pycharm

## Section 3

Telegraf

### telegraf install in Windows
	1) install as a service via command prompt "telegraf.exe -service install -config <absolute_path_to_config>"
	2) config file:
		a) for multiple instances with same process name, such as WmiPrvSE, enable wildcards as below:
		     [[inputs.win_perf_counters]]
				UseWildcardsExpansion=true
			[[inputs.win_perf_counters.object]]
				ObjectName = "Process"
				Counters = [...]
				Instances = ["WmiPrvSE*"]
		b) for file output locally
			[[outputs.file]]
			## Files to write to, "stdout" is a specially handled file.
				files = ["stdout", "/tmp/metrics.out"]
	3) 