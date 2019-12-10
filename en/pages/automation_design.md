# Automation Design


## Object Oriented Class Building Block



### Remote running
 [VMWare setup](vmware-setup.md)


# Python

## Tips:
	- Determine python interpreter version is 32bit or 64bit, go to interactive mode, it will show bit information
	- Determine architecture is 32bit or 64bit, go to interactive mode, then:
		import platform
		platform.architecture()	
	- python 64bit matplotlib import issue "ImportError: DLL load failed: %1 is not a valid Win32 application" after switching from python 32bit interpreter
		reinstall numpy and matplotlib will fix it
	- python pip import error:
		python -m ensurepip
		or download get-pip.py as https://stackoverflow.com/questions/4750806/how-do-i-install-pip-on-windows
	Refer to https://wiki.absolute.com/pages/viewpage.action?pageId=13369722 for VM setup.

## Pycharm Tips:
	- Resolve Warning import local package: Unresolved references inspection in Pycharm
	    Go to the settings "Ctrl+Alt+S" or Project-> Project Structure, and select the next options
		Select the folder which want to be the source tag (Content Root), then right click to mark as Source

Automation tips
