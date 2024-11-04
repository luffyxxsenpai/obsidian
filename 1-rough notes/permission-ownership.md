# permission-ownership
---
Date: 02,Oct,2024
subject: using chmod and chown to manage permissions 
field: [[linux]]
tags:  #chmod #chown

---

its very important  to understand  how user and group permission work

a simple ls -l output
`-rw-r--r-- root root  0 B Mon Sep 23 13:25:52 2024 a
`-rw-r--r-- root root  0 B Mon Sep 23 13:25:52 2024 b
`-rw-r--r-- root root  0 B Mon Sep 23 13:25:52 2024 c
`drwxr-xr-x root root 10 B Mon Sep 23 13:26:05 2024 d
`drwxr-xr-x root root 10 B Mon Sep 23 13:26:05 2024 e

`drwxr-xr-x = in this d represent its a directory
`-rw-r--r-- = in this a dash at start represent its a file

it is divided in 4 part
-  -rwx -r- r-- = type -user-group-others 
r = read
w = write
x = execute

# HOW TO MODIFY THE PERMISSIONS
chmod is used to change the permission of a file or directory

*I DONT PREFER THIS ABCD WAY , I LIKE OCTAL WAY

`chmod 764 file.txt
7 = user
6 = group
4 = others

now these numbers are a combination of rwx permissions  where
0 = no permission
1 = execution
2 = write 
4 = read 

we can add these numbers according to our permissions like
if we want only read and write = 2+4= 6
if we want read write and exec = 1+2+4 = 7

`chmod 764 file.txt will give 
user = full permission
group = read and write
other = read only

#### OWNERSHIP
**ownership** refers to the relationship between users and the files or directories they create and manage. Every file and directory in Linux has three main attributes: the **owner**, the **group**, and **others**, each of which can have specific permissions to control access and actions.

`sudo chown [OPTIONS] NEW_OWNER:NEW_GROUP FILE

`sudo chown luffy:dev myfile.txt = will make luffy owner of the file and anyone from dev group 

`sudo chown -R luffy:dev a.txt = -R will recursively change permissions

`sudo chgrp dev a.txt = this command will explicitely change the group only

`.rwxrw-r-- luffy dev 46 B Mon Sep 23 14:07:37 2024 testfile

in this file, i created it as root then changed it owner and group as luffy and zoro, now luffy can do anything with this file, where group will only be able to read and write. you can try adding another user in dev group, that user will also have rw permission.
and other users who are not in the group will only be able to read it.


### GETFACL and SETFACL
ACL (access control list) is a more advance way to have more refined control over permissions

`.rw-rw-r--+ luffy luffy  0 B Mon Sep 23 15:43:15 2024 hi
the + sign shows acl has been applied on this file

```

before
└─$ getfacl hi   
 file: hi
owner: luffy
 group: luffy
user::rw-
group::rw-
other::r--


after
sudo getfacl hi
 file: hi
 owner: luffy
 group: luffy
user::rw-
user:zoro:rw-
group::rw-
mask::rw-
other::r--

well this is quite an avdance shit so i am gonna skip it for now
```



