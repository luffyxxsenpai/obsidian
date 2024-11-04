# users-group-in-linux
---
Date: 02,Oct,2024
subject: users and group in linux 
field: [[linux]]
tags: #user #group #usermod #useradd 

---
in a multi user system like servers, it is very important to have a  controlled environment to manage and control the users.
in linux, the user with highest access level is called root 

you can use this command to see all the users present in the system
`cut -d: -f1 /etc/passwd

all users have their user id where root is 0 , system users will be 1 to 999 , standard users will start from 1000 by default which we can change later 
```bash
cat /etc/passwd/

root:x:0:0:root:/sec/root:/bin/zsh
luffy:x:1000:1000:luffy:/home/luffy:/usr/bin/zsh
username : hashed passwd : UID : GID : user-info : home directory : shell
```

`sudo useradd -g groupname -s /bin/bash -c "myuser" -m -d /home/userdir username



now many distro configre default useradd action accroding to them
*cat /etc/default/useradd* shows the default behavior of useradd command 
now you dont need to edit this file, just be more specific in your command

#### useradd
- useradd command is used to add users
- we have many options when making a user

```bash
sudo useradd zoro = will add user zoro

sudo useradd -u 1009 zoro = will set custom uid

sudo useradd -M luffy = add user without home directory

sudo useradd -s /bin/zsh zoro = will set the shell

sudo useradd -s /usr/bin/nologin zoro = it will add user without a shell so user can not login 

sudo useradd -c "mr zoro" zoro = add a description 

sudo useradd -m zoro = add home directory at /home/

sudo useradd -m -d /abc luffy = will create a user with custom home path
(-d specify the path but -m helps creating that location)

sudo useradd -r sysuser = will add user as a system user

sudo passwd zoro = will set the password for zoro user
```


#### usermod
- after creating a user, sometimes we need to modify the user account and for that we use usermod

```bash
sudo usermod -s /bin/zsh zoro = will set the shell

sudo usermod -l new-username old-username = change username

sudo usermod -u 7878 luffy = modify the uid of luffy

sudo usermod -d /new/home/directory username = will change user home directory

sudo usermod -L user = locks the user account, cant login



sudo usermod -U user = unlocks the account 

sudo userdel zoro = delete the user

sudo userdel -f zoro = forcefully delete user if he is logged in

sudo userdel -r zoro = will remove the user and its home directory

```



#### groups
- **groups** are a way to organize users into collective units for the purpose of managing permissions and access to resources more efficiently. Each user can belong to one or more groups
- there are 2 types of group, primary and secondary group 
- when we create a user a primary group is added to user, by default its username
- secondary groups are additional group a user can be part of
- you can see all available groups by `cat /etc/group`

```bash
groups = will show you the groups you are a member of
groups zoro = will show groups of user zoro
groupadd mygroup = will create a new group
groupdel mygroup = will delete a group
groupmod -n newgroup mygroup = change name of a group

usermod -aG mygroup,yourgroup,newgroup zoro = will add user zoro in these groups

usermod -g groupname user  = to change the default group of a user

gpasswd -d zoro mygroup = will remove a user from group

```


