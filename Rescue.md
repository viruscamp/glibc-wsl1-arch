# Rescue

How to rescue a distro in WSL1 which glibc is broken.

## Static Busybox and Pacman
### Installation
```bash
sudo pacman -S busybox
git clone https://aur.archlinux.org/pacman-static.git
cd pacman-static
makepkg
sudo pacman -U pacman-static-*.zstd
```
### Using
1. In Windows, download a working glibc from [Arch Archive](https://archive.archlinux.org/packages/g/glibc/)  
2. In cmd or powershell, enter busybox shell in WSL  
    ```
    wsl -d ArchWSL1 -e /usr/bin/busybox sh
    ```
3. In busybox shell  
    ```bash
    pacman -U /mnt/c/Users/Your/Downloads/glibc-*.tar.zstd
    ```

## Another WSL1 distro
### [miniwsl](https://github.com/0xbadfca11/miniwsl)

## Manipulate WSL1 file in windows
### [wslattr](https://github.com/viruscamp/wslattr)
### [lxssattr](https://github.com/dmex/lxssattr)
