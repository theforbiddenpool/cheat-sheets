### Save File as `root` While `vim` editing
```
:w !sudo dd of=shellescape(expand('%'))
```

### Get Fastest Mirrors
```
$ sudo reflector --latest 5 --sort rate --protocol https --save /etc/pacman.d/mirrorlist
```

### Restart xinit
```
$ sudo xinit -- :2
```

### Make a Backup Using `rsync`
```
$ sudo rsync -acAXvP --delete --exclude=/dev/* --exclude=/proc/* --exclude=/sys/* --exclude=/tmp/* --exclude=/run/* --exclude=/mnt/* --exclude=/media/* --exclude=/lost+found --exclude=~/.local/share/Steam/steamapps/common/* / /mnt/backup-disk
```

### Manually Install AUR Package
```
$ cd ~/Programs/
$ git clone <aur-package-url>
$ cd <program>
```

Check if `PKGBUILD` file is there. We can edit or verify it if we want.
```
$ makepkg -si
```

### Access `.backup` android file
```
dd if=userdata_20150101_000026.backup skip=512 bs=128k iflag=nocache,skip_bytes oflag=nocache,append conv=notrunc of=img.ext4
dd if=userdata_20150101_000026.backup1 ...
```

Extract it using **7zip**:
```
7x x img.ext4
```

### Keyboard Layouts Folder
`/usr/share/X11/xkb/symbols/`

### Create new NTFS file system
```
mkntfs -Q -v -F -L 'Label' '/dev/sdd1'
```

## Systemctl
Unit = Deamon\
Enable → means start with boot

_Check if unit is enabled:_
```
$ systemctl is-enabled <name-unit>
```

_Enable unit:_
```
$ sudo systemctl enable <name-unit>
```

_Disable unit:_
```
$ sudo systemctl disable <name-unit>
```

_Start unit:_
```
$ sudo systemctl start <name-unit>
```

_Restart unit:_
```
$ sudo systemctl restart <name-unit>
```

_Stop unit:_
```
$ sudo systemctl stop <name-unit>
```

_Check unit status:_
```
$ sudo systemctl status <name-unit>
```
- `-l` → show more information

_List all units installed:_
```
$ systemctl list-units
```

_Reload all units:_
```
$ systemctl deamon-reload
```

### Viewing logs with `journalctl`
_View log for specified unit:_
```
$ sudo journalctl -u <name-unit>
```

_Show all messages from last boot:_
```
$ sudo journalctl -b
```

_Follow new messages:_
```
$ sudo journalctl -f
```
