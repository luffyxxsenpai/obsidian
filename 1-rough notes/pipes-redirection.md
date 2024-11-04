# pipes-redirection
---
Date: 03,Oct,2024
subject: pipes and redirection 
field: [[linux]]
tags: #pipe #redirection

---
### STDIN STDOUT STDERR

- `stdin` stands for **standard input**, which is the stream from which a program reads its input. By default, this is usually the keyboard, but `stdin` can also come from files or other programs through redirection.
    - When you run a command that requires input, it waits for data from `stdin`. For instance, when you use the `cat` command without specifying a file, it reads input from the terminal (keyboard) until you signal the end of input (usually with `Ctrl + D`).
   
-  `stdout` stands for **standard output**, which is the stream where a program writes its output. By default, `stdout` is connected to the terminal (display).
    - Whenever a program produces output (e.g., results from a computation or messages), it writes to `stdout`. This output is usually displayed in the terminal unless redirected.

- `stderr` stands for **standard error**, which is a stream used specifically for error messages. By default, it is also connected to the terminal, but it's separate from `stdout` so that regular output and error messages can be handled differently.
    - When a program encounters an error or needs to display diagnostic messages, it writes to `stderr`. This allows for error messages to be displayed separately from regular program output.

	stdin: 0     <
	stdout: 1   >
	stderr: 2    2>

## HOW WE USE IT 

- we can redirect these 3 in different ways
- some output can be input of something 

```bash

cat > a.txt = will create a empty file 

echo "hello" > a.txt = output of echo will be redirected as input of a.txt

echo "hello again" > a.txt = output of echo will be APPENDED as input of a.txt

cat < a.txt = input of cat will be a.txt


catt a.txt > b.txt 2> error.txt

2> is used to redirect error

if i want to redirect output and error both in 1 file i can do


cat a.txt > b.txt 2>&1 
this will redirect both error and output in b.txt

```



