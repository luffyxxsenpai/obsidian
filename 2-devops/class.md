1. bios -> do post and locate bootloader 
2. bootloader -> locate kernel from /boot into memory and initramfs or initrd
4. kernel -> initializing the cpu memory and hardware -> mount initramfs -> initialize hardwares -> mount root filesystem 
4. PID 1 /etc/systemd/system/  -> network manager, login services , device initializations 
5. userspace initalization 
6. 


'' initramfs helps kernel to access real root fs by providing necessasary drivers and tools in a compressed ormat ''  once kernel mounts the real root fs  its discarded 
cause of modular kernels

compiled components in kernel core is like tcp/ip stack , fs support etc



mbr 
446 byte  4partition  2tb max ,  only starting 

gpt
guid, 128 partitiobs , data at beginning and end , 

kernel
monolithic = fast context switching = 

microkernel = basic system service lke IPC and hardware abstraction / 
device driver , fs in userspace theretically 
systemcalls context switching / networking stack 


kernel space and userspace 
security / stability / efficiency

