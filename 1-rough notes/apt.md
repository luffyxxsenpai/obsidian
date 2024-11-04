# apt
---
Date: 01,Oct,2024
subject: apt 
field: [[linux]]
tags: #apt #rollback #ubuntu #debian

---
# what is apt
- apt stands for `Advance Package Tools`
- its is a package management tool used in debian based distributions like ubuntu, mint, pop etc.
- it is a wrapper over dpkg which is a low level package manager in debian based distros
- apt automatically handles package dependencies
- apt maintains a local cache of package information helping in faster package searches and updates


### apt file locations

1. repository configuration: `/etc/apt/sources.list`
2. additional repository source: `/etc/apt/sources.list.d/`
3. lock files: `/var/lib/apt/lists/lock`, `/var/cache/apt/archives/lock`
4. apt configuration: `/etc/apt/apt.conf`
5. GPG Keys [[gpg-key]] : `/etc/apt/trusted.gpg`, `/etc/apt/trusted.gpg.d/`
6. Installed Package Status: `/var/lib/dpkg/status`
7. deb file archives: `/var/cache/apt/archives/`

### apt commands

**apt vs apt-get**
- apt is a modern replacement of apt-get
- apt shows a progress bar, number of packages needs to be updated while apt-get doesn't
- apt automatically resolve dependencies conflicts, apt-get doesn't 
- it is advisable to use apt instead of apt-get
- apt combines multiple commands like apt-get, apt-cache, dpkg -i [[dpkg]]


1. update the installed package database with latest available versions from repository
	`sudo apt update`

2. upgrade the locally installed packages with the latest update 
	`sudo apt upgrade`
	
3. install the mentioned package name from the repo
	`sudo apt install nginx`
	
4. if nginx is installed already and theres an update then only upgrade, it wont install or update if nginx is not already installed in system
	`sudo apt install nginx --only-upgrade`
	
5. install a specific version of nginx
	`sudo apt install nginx=1.18.0-0ubuntu1`

6. it will only remove the binary of nginx and keep the conf, dependencies and other files related to it 
	`sudo apt remove nginx`

7. purge will remove binary and the configuration files also but will keep the dependencies, it will not remove any conf file from user home directory 
	`sudo apt purge nginx`

8. shows the information about the package
	`sudo apt show nginx`

9. shows the list of all the available package from the repo
	`sudo apt list`

10. shows only the installed package 
	`sudo apt list --installed`

11. search a package from the repo 
	`sudo apt search docker`

12. this removes the orphaned dependencies which were installed with some package and are no longer used
	`sudo apt autoremove` 

13.  resolve any missing dependencies or broken package while installation or half-installed system state
	`sudo apt --fix-broken install`

14. apt stores package file in (/var/cache/apt/archives/) when we install or update software and overtime it accumulates so this will remove those outdated .deb files which are no longer required
	`sudo apt autoclean`

15. apt can install deb packages like [[dpkg]] but dpkg can't automatically resolve dependencies like apt can 
	`sudo apt install package.deb`

16. stop apt from automatically upgrade a package
	`sudo apt-mark hold nginx`

17. APT does not provide a straight forward rollback method but we can 
	-  downgrade to  a specific or older version of that app
	- hold the future update of that package 
	- list out older package file from /var/cache/apt/archives and install directly from the archive 
		`dpkg -i /var/cache/apt/archives/nginxyz.deb`
	
---
