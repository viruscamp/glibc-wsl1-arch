# Rescue

How to rescue a distro in WSL1 which glibc is broken.

## Static Busybox and Pacman
### Not Prepared
In Windows:
1. `mkdir c:\wsl`, make sure current user has read/write permissions
2. download the attach from [issue#1](https://github.com/viruscamp/glibc-wsl1-arch/issues/1), extract it to `c:\wsl`
3. download a working glibc to `c:\wsl` from [Arch Archive](https://archive.archlinux.org/packages/g/glibc/)
4. Open a cmd console, run `wsl -d Arch -u root -e /mnt/c/wsl/busybox sh`
5. Now you can use `/mnt/c/wsl/pacman-static -U /mnt/c/wsl/glibc-*.tar.zst`

### Prepared Installation
```bash
sudo pacman -S busybox
git clone https://aur.archlinux.org/pacman-static.git
cd pacman-static
makepkg
sudo pacman -U pacman-static-*.zstd
```
### Prepared Using
1. In Windows, download a working glibc from [Arch Archive](https://archive.archlinux.org/packages/g/glibc/)  
2. In cmd or powershell, enter busybox shell in WSL  
    ```
    wsl -d ArchWSL1 -u root -e /usr/bin/busybox sh
    ```
3. In busybox shell  
    ```bash
    pacman-static -U /mnt/c/Users/Your/Downloads/glibc-*.tar.zstd
    ```

## Another WSL1 distro
### [miniwsl](https://github.com/0xbadfca11/miniwsl)

## Manipulate WSL1 file in windows
### [wslattr](https://github.com/viruscamp/wslattr)
### [lxssattr](https://github.com/dmex/lxssattr)

