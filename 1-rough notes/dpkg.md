# DPKG
---
Date: 02,Oct,2024
subject: dpkg 
field: [[linux]]
tags: #dpkg #apt #rollback #ubuntu #debian 

---
dpkg is a package management system for Debian-based Linux distributions. It is used to install, remove, and manage software packages in the system. The dpkg command is responsible for handling the low-level details of package management, such as unpacking and installing packages, configuring packages, and maintaining a database of installed packages.
dpkg is the underlying tool APT[[apt]] uses.

- direct control over package management
- works offline since it does not provides dependency resolution
- no interaction with apt repository or any repo, it only interacts with local deb files
- cannot upgrade packages automatically
- no search or query feature
- dpkg uses the  ***`.deb`*** format
- dpkg can remove any installed package even if it was installed through APT

## dpkg command

1. to install a package
	`sudo dpkg -i nginx.deb`
	
2. to remove a package 
	`sudo dpkg -r nginx`
	
3. to purge a package
	`sudo dpkg -P nginx`
	
4. to list all the installed package
	`sudo dpkg -l`

5. to check if package is installed
	`sudo dpkg -l nginx`

6. to see information about a package
	`dpkg -s nginx`