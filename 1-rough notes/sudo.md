# sudo
---
Date: 02,Oct,2024
subject: how to use sudo 
field: [[linux]]
tags: #sudo #linux #root

---

# how to switch user

`su - username = will swtich user completely with their home 
`su username = will just switch user in the current directory you were in
`su - = without any option it will swtich to root

# SUDO 
its a way to grant a user superuser/root user permission temporarily
to run a command as sudo, you need to be either root user or in sudoers wheel group

- details of sudo is present in /etc/sudoers, to edit his file run "visudo"

- to give a user sudo access you weould need to add them in wheel group

`sudo usermod -aG wheel myuser (redhat derivatives use wheel)
`sudo usermod -aG sudo myuser (ubuntu use sudo)

now this will give you complete access of sudo

but if u want to limit the access of sudo to particular commands you can do that

open sudoers file
`add "  luffy    ALL=UPDATE,SYSCTL  "
and create a command alias 
`"  Cmnd_Alias UPDATE = /usr/bin/apt  "
`"  Cmnd_Alias SYSCTL = /usr/bin/SYSTEMCTL  "

you can now fine grain the sudo access control for any user
