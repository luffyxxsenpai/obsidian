# find
---
Date: 03,Oct,2024
subject: find any file in linux 
field: [[linux]]
tags: #find #locate

---

- find command is used to find any thing on your Linux system.
- find comes in 2 different version, one GNU and another OpenBSD
- find has many flags but heres the most easy and normal one

**FIND     LOCATION    FLAGS**

1. find the file named 'findthisfile.txt' from the current directory
	`find . -name "findthisfile.txt"`

2. find the same file but with case insensitivity 
	`find . -iname "findthisfile.txt"

3. we can define the type we r looking for, like a file or directory, f = file, d= directory, l = symbolic link
	`find . -type f -name "findthisfile.txt"

4. we can filter out the user who owns the file
	`find . -type f -user luffy -name "findthisfile.txt"

5.  we can exec some command after finding our file, this will find the file which has this line inside it.
	`find  . -name "*.txt" -exec grep -l  "this line is hidden in a file" {} +   = find the file which has this line inside it

6. we can find using size  (+ = greater, - = smaller) (c,k,M,G)  = bytes, kb, mb, gb , this will find the files greater than 1gb and then exec du to tell us the exact size
	`find . -size +1G -exec du -sh {} + 2> /dev/null`

7. we can filter out somethings by using permission 
	`find . -perm 777 `

- we can redirect permission error to stderr

