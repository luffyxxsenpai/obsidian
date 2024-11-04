# du-df
---
Date: 07,Oct,2024
subject: space management 
field: [[linux]] 
tags: #du #df 

---

**while du shows the information about filesystem, df shows us what files or directories are filling that filesystem. if df is high level then du is low level**


# df
- df = disk free
- it shows the amount of available disk space on file system

1. without option it will show usage of all mounted fs
	`df`

2.  by default shows 1k blocks, use -h for human readable
	`df -h `

3. display type of file system
	`df -T`

4. display inodes usage
	`df -i `

5.  display usage of fs by giving some dir path of that fs
	`df -h /`

6.  show total of all fs
	`df -h --total`



# du
- du = disk usage
- used to display file space usage

1. by default it will show size of current dir and subdir
	`du`

2. human readable
	`du -h`

3.  summarize total 
	`du -sh /path/to/dir`

4.  show size of each file , default only shows the dir
	`du -ah /path/to/dir`

5. Limit the Depth of Subdirectories
	`du -ha --max-depth=1 /mnt/lab`

6. show grand total with list of files
	`du -hc /path/to/dir`

7.  exclude certain file using pattern
	`du -hac --exclude="*.mkv" /mnt/lab`

8. show size of a specific file
	`du -h file.txt`

9.  show in MB or GB (-BM, -BG)
	`du -BM /path/to/dir`

