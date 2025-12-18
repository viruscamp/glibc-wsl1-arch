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
```powershell
wsl -d ArchWSL1 -e /usr/bin/busybox sh
```

## Another WSL1 distro
### [miniwsl](https://github.com/0xbadfca11/miniwsl)

## Manipulate WSL1 file in windows
### [wslattr](https://github.com/viruscamp/wslattr)
### [lxssattr](https://github.com/dmex/lxssattr)
