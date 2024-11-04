# text manipulation and viewing
---
Date: 04,Oct,2024
subject: viewing and manipulation of texts  
field: [[linux]]
tags: #cat #grep #awk #head #tail #less #more #sed #egrep #cut #sort #wc #uniq #tr #xargs

---
cat more less sort head tail grep

viewing and manipulating texts based stuffs are very important in linux and these are some of the most used commands used for this purpose and very useful in scripting

## CAT :LiHeart:
a simple command to see the content of some file.
1. see content of a file
	`cat a.txt`
2. see content of multiple files
	`cat a.txt b.txt`
3. see number lines 
	 `cat -n a.txt`
4. only show number lines on non-blank lines
	`cat -b a.txt`

## MORE
a command to see content of larger files page by page 

`more a.txt`
- **SPACE**: Move to the next page.
- **ENTER**: Scroll down line by line.
- **b**: Move back one page.
- **q**: Quit `more`.
- **/**: search a term


## LESS
- less is better than more to see content of some file
- unlike MORE LESS does not load the entire file into memory
	`less a.txt`
- - **SPACE**: Move to the next page.
    - **ENTER**: Scroll down one line.
    - **b**: Move back one page.
    - **Up/Down Arrow keys**: Move up/down line by line.
    - **g**: Go to the beginning of the file.
    - **G**: Go to the end of the file.
    - **q**: Quit `less`.
- **Search within the file**:
    - **/**: Search forward by entering a string.
    - **n**: Move to the next occurrence of the search term.
    - **N**: Move to the previous occurrence of the search term.


## SORT
sort just sort out lines of text from some file or some redirected output. [[linux]]
sort is quite powerful but surely we don't need the whole power mostly

1. sort by default sort out alphabetically
	`sort file.txt
2. sort can sort out in reverse order
	`sort -r file.txt`
3. to sort numerical content
	`sort -n file.txt`
4.  remove duplicate lines
	`sort -u file.txt`
5.  specify an output file
	`sort file.txt -o sortedfile.txt         `

 

## HEAD
head is used to display the top of a file, by default it shows first 10 lines

1. simply see first 10 lines of a file
	`head file.txt`

2. specify a specific number of lines 
	`head -5 file.txt OR head -n 5 file.txt`

3. get a head from multiple files 
	`head a.txt b.txt`

4. when doing head for multiple files it shows the file name, it comes from another option `-v` which forces itself when doing multiple file, to suppress we can use `-q`
	` head -q a.txt b.txt`



## TAIL
tail is used to display the bottom of the file, by default it also shows 10 lines

1. simply see last 10 lines of a file
	`tail file.txt`

2. specify a specific number of lines 
	`tail -5 file.txt OR tail -n 5 file.txt`

3. get a tail from multiple files 
	`tail a.txt b.txt`

4. real time monitoring using tail
	`tail -f a.txt`

5. monitor 2 files at the same time
	`tail -f /var/log/syslog /var/log/auth.log`

6. start from a specific line number
	`tail -n +2f a.txt`



## GREP
- Global Regular Expression Print
- it search for a particular string or keyword from a file and print the matching output
- it checks line by line and print lines matching given pattern
- **GREP [OPTION]   [PATTERN]  FILE**

1. search something from the file 
	`grep luffy a.csv`

2.  case insensitive search
	`grep -i luffy a.csv`

3. search everything except out given pattern
	`grep -v luffy a.csv`

4.  search for the exact pattern
	`grep -w luffy a.csv`

5.  count the number of times pattern matched
	`grep -c luffy a.csv`

6. see at which line number you are getting the match
	`grep -n luffy a.csv`

7.   search in multiple file (can use -h to suppress file name)
	`grep luffy a.csv b.csv`

8.  to have multiple search pattern
	`grep -ie luffy -e zoro a.csv`

9. only get the file name if pattern matches
	`grep -l luffy a.csv`


## SED

- SED - stream editor
- after s , we give our delimiter which normally is /

1. replace a text
	`sed 's/og/new/ ' a.txt`


1. save the output
	`sed -i 's/og/new/' a.txt `


1. for the global substitution 
	`sed -i 's/og/new/g' a.txt `


1. 
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`


1. a
	`a`

