# Known Issues

https://wsldl-pg.github.io/ArchW-docs/Known-issues

1. termios2  
WSL1 does not support termios2 (ioctl cmd: TCGETS2, TCSETS2, TCSETSW2 and TCSETSF2), but glibc 2.42 switches to termios2.  
working [glibc-2.41-r65](https://archive.archlinux.org/packages/g/glibc/glibc-2.41%2Br65%2Bge7c419a29575-1-x86_64.pkg.tar.zst)  
https://github.com/microsoft/WSL/issues/2595  
https://github.com/microsoft/WSL/issues/13378  
fix: [OneBlue said in 2025-10-11](https://github.com/microsoft/WSL/issues/13378#issuecomment-3392573154)  

2. memfd_create  
https://github.com/microsoft/WSL/issues/3542  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#fakeroot  
use fakeroot-tcp instead fakeroot  

3. `.note.ABI-tag`=`GNU/Linux 4.11.0`  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#qt5  
qt5-base qt6-base  
strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5  

4. AIO  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#mysql-8mariadb  
MySQL 8/MariaDB  

5. **fixed** sleep: cannot read realtime clock: Invalid argument  
https://github.com/microsoft/WSL/issues/4898  
working glibc-2.30-3  
fix: [20H2 Build 19042.487 (KB4571744)](https://github.com/microsoft/WSL/issues/4898#issuecomment-682109141)  

6. **fixed** unsupported syscall TIME64 FACCESSAT2  
working glibc-2.33-3  
https://github.com/yuk7/ArchWSL/issues/190  
https://aur.archlinux.org/cgit/aur.git/tree/glibc-linux4.patch?h=glibc-linux4  
fix: The official glibc-2.38 reported to work in WSL1  

<details>
<summary>unsupported SYSCALLS</summary>
```
# define __ASSUME_TIME64_SYSCALLS 0
# define NO_ASSUME_TIME64_SYSCALLS 1

futex_time64
clock_adjtime64
clock_getres_time64
clock_nanosleep_time64
clock_settime64
mq_timedreceive_time64
mq_timedsend_time64
recvmmsg_time64
sched_rr_get_interval_time64
ppoll_time64
pselect6_time64
timer_gettime64
timer_settime64
timerfd_gettime64
timerfd_settime64
utimensat_time64

pselect64_syscall (nfds, readfds, writefds, exceptfds, timeout, sigmask);
semtimedop_syscall (semid, sops, nsops, timeout)

# define __ASSUME_FACCESSAT2 0
faccessat2
```
</details>
