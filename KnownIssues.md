# Known Issues

https://wsldl-pg.github.io/ArchW-docs/Known-issues

1. termios2  
WSL1 does not support termios2 (ioctl cmd: TCGETS2, TCSETS2, TCSETSW2 and TCSETSF2), but glibc 2.42 switches to termios2.  
https://github.com/microsoft/WSL/issues/2595  
https://github.com/microsoft/WSL/issues/13378  
affects: `glibc` `bash`  
latest working version: [glibc-2.41-r65](https://archive.archlinux.org/packages/g/glibc/glibc-2.41%2Br65%2Bge7c419a29575-1-x86_64.pkg.tar.zst)  
workground: [this repo: glibc-wsl1](https://github.com/viruscamp/glibc-wsl1-arch)  
fix: [OneBlue said in 2025-10-11](https://github.com/microsoft/WSL/issues/13378#issuecomment-3392573154)  

2. SYSV IPC  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#fakeroot  
fakeroot is using SYSV IPC by default. but WSL1 does not support it now.  
affects: `fakeroot`  
workground: use [fakeroot-tcp](https://aur.archlinux.org/packages/fakeroot-tcp)  

3. memfd_create  
https://github.com/microsoft/WSL/issues/3542  
affects: `nginx`  
workground: no  

4. `.note.ABI-tag`=`GNU/Linux 4.11.0`  
https://github.com/Microsoft/WSL/issues/3023  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#qt5  
affects: `qt5-base` `qt6-base`  
workground: `strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5`  

5. AIO  
https://wsldl-pg.github.io/ArchW-docs/Known-issues/#mysql-8mariadb  
affects: `mariadb` MySQL8   
workground: disable AIO in configfile  
    ```
    [mysqld]
    innodb_use_native_aio=0
    ```

6. landlock  
Got 'error: restricting filesystem access failed because landlock is not supported by the kernel!', when using pacman.  
https://github.com/AzureZeng/wsl-arch-rootfs/issues/2  
affects: pacman  
workground: Add `DisableSandbox` to '/etc/pacman.conf'  

7. 'Failed to take /etc/passwd lock: Invalid argument'  
Got 'Failed to take /etc/passwd lock: Invalid argument', when using apt or pacman.  
Failed at `fcntl(3, F_OFD_SETLKW,..)` of `systemd-sysusers`.  
https://github.com/microsoft/WSL/issues/10397  
affects: apt pacman systemd  
workgroud:  
  - Arch: ignore it  
  - Debian/Ubuntu: `cd /bin && mv -f systemd-sysusers{,.org} && ln -s echo systemd-sysusers`  

8. **fixed** sleep: cannot read realtime clock: Invalid argument  
https://github.com/microsoft/WSL/issues/4898  
affects: `glibc`  
latest working version: glibc-2.30-3  
fix: [20H2 Build 19042.487 (KB4571744)](https://github.com/microsoft/WSL/issues/4898#issuecomment-682109141)  

9. **fixed** unsupported syscall TIME64 FACCESSAT2  
https://github.com/yuk7/ArchWSL/issues/190  
https://aur.archlinux.org/cgit/aur.git/tree/glibc-linux4.patch?h=glibc-linux4  
affects: `glibc`  
latest working version: glibc-2.33-3  
fix: when glibc-2.38 released about 2023-8  
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
