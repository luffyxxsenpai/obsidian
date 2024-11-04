# DNF
---
Date: 02,Oct,2024
subject: yum/dnf 
field: [[linux]]
tags: #dnf #linux #red-hat

---
- dnf is another high level package manager for fedora/red-hat based distribution like centos, rocky linux
- dnf stands for **DANDIFIED YUM** 
- dnf is a modern replacement for yum, both can be used but dnf preffered
- dnf uses RPM as its underlying technology 

### dnf commands

1. to search a package from the repositoy
   `dnf search nginx`

2. to install a package 
   `dnf install nginx`

3. to remove a package
   `dnf remove nginx`

4. to get the info about a package
   `dnf info nginx`

5. to see which package provides some specific command or package
   `dnf provides `

6. update a specific pacakge
   `dnf update nginx`

7. check for updates
   `dnf check-update`

8. update all the package
   `dnf update`

9. list installed package
   `dnf list installed`

10. list available package
   `dnf list availabe`

11. list enabled repo
   `sudo dnf repolist

12. list all repo 
   `sudo dnf repolist all`

13. clear cache including metadata, downloaded packages
   `sudo dnf clean all`

14. autoremove unneeded package
   `sudo dnf autoremove`

15. install  a package group
   `sudo dnf group install groupname`

16. remove a package group
   `sudo dnf group remove groupname`

17. downgrade a package
   `sudo dnf downgrade nginx`

18. install a rpm package
    `sudo dnf install ./nginx.rpm`



