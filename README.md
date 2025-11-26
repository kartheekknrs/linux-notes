### Table of contents

1. Basics & environment
2. Filesystem navigation & file ops
3. File viewing & processing
4. Permissions & ownership
5. Text editing and editors
6. Searching (find/grep/locate)
7. Compression & archiving
8. Package management (apt/yum/dnf/pacman/rpm/dpkg)
9. Users & groups
10. Processes & job control
11. Systemctl & services
12. Networking
13. Disk, partitions & filesystems
14. Logs & journal
15. Boot & kernel
16. Security: sudo, SELinux, AppArmor
17. Bash shell basics & scripting utilities
18. Misc tools (curl/wget/rsync/screen/tmux)
19. Troubleshooting & debugging
20. Handy combos & best practices

## 1. BASICS & ENVIRONMENT

* pwd — print working directory

* whoami — current user

* id — user and groups

* hostname — show hostname

* uname -a — kernel & machine info

* env — show environment variables

* printenv VAR — print specific env var

* export VAR=value — set environment variable for current shell

* set — list shell variables

* clear — clear terminal

* date — show current date/time

* uptime — how long system has been up, load averages

* cal — calendar

* arch or uname -m — CPU architecture

## 2. FILESYSTEM NAV & FILE OPERATIONS

* ls — list files

  * ls -l  — long listing
  
  * ls -la — show hidden files
  
  * ls -lh — human-readable sizes
  
  * ls --color=auto  — colored output

* cd /path/to/dir — change directory

* mkdir dir — create directory

  * mkdir -p a/b/c — create parents as needed

* rmdir dir — remove empty directory

* cp src dest — copy files

  * cp -r dir1 dir2 — recursive copy
  
  * cp -a — preserve attributes (archival)

*  mv src dest — move or rename

* rm file — delete file

  * rm -r dir  — recursive
  
  * rm -f  — force
  
  * rm -rf  — dangerous: force recursive

* ln -s target linkname — create symbolic link

* stat file — detailed file metadata

* file filename — guesses file type

* touch file — create empty file or update timestamps

## 3. FILE VIEWING & PROCESSING

* cat file — dump file to stdout

* tac file — reverse file

* nl file — number lines

* less file — pager (use q to exit)

  * less +F file — follow mode (like tail -f)

* more file  — older pager

* head -n 10 file — first lines

* tail -n 10 file — last lines

  * tail -f file — follow appended content

* cut -d',' -f1 — cut fields by delimiter

* sort — sort lines

  * sort -n — numeric
  
  * sort -r — reverse

* uniq — remove adjacent duplicates

  * sort | uniq -c — count unique lines

* tr 'a-z' 'A-Z' — translate characters

* wc — word/line/byte count

  * wc -l  — count lines

* tee file — write to stdout and file

* split -b 10M bigfile — split into 10MB chunks

* paste file1 file2 — merge columns

## 4. PERMISSIONS & OWNERSHIP

* ls -l — shows permissions (rwx)

* chmod — change permissions

  * symbolic: **chmod u+rwx,g+rx,o-r** file
  
  * numeric: **chmod 755 file** (u=rwx (7), g=rx (5), o=rx (5))
  
  * special bits: setuid (4___), setgid (2_), sticky bit (_1)
  
    * e.g. **chmod 4755 /path/to/binary** (setuid)

* chown user:group file — change owner and group

* chgrp group file — change group only

* umask — default permission mask for new files

  * umask 022 means new files 755/644 style

* getfacl file / setfacl — get/set POSIX ACLs for fine-grained perms

## 5. TEXT EDITORS

* **vi filename** or **vim filename** — modal editor

 * common: i insert, Esc, :w save, :q quit, :wq save+quit, :qa! quit all
 
 * visual mode, yank (y), paste (p), delete (d)

* nano file — user-friendly editor (Ctrl+O save, Ctrl+X exit)

* emacs file — powerful editor

## 6. SEARCHING — find / grep / locate

* find /path -name "*.log" — find files by name (case-sensitive)

* find /path -iname "*.Log" — case-insensitive

* find . -type f -mtime -7 — modified within last 7 days

* find . -type f -size +100M — files bigger than 100MB

* find . -name "*.tmp" -exec rm {} \; — execute command on results

* locate filename — fast DB-backed search (update DB with updatedb)

* grep 'pattern' file — search text

 * grep -R "TODO" . — recursive search
 
 * grep -n show line numbers
 
 * grep -i ignore case
 
 * grep -E extended regex
 
 * grep -P perl regex (if supported)
 
 * zgrep for gzipped files

* egrep (equiv. grep -E)

## 7. COMPRESSION & ARCHIVING

* tar -cvf archive.tar dir/ — create tar

* tar -xvf archive.tar — extract tar

* tar -czvf archive.tar.gz dir/ — create gzip tar

* tar -xzvf archive.tar.gz — extract gzipped tar

* tar -cjvf archive.tar.bz2 dir/ — bzip2

* tar -xJvf archive.tar.xz — xz

* gzip file -> file.gz; gunzip to extract

* zip -r archive.zip dir/ and unzip archive.zip

* 7z a archive.7z files if p7zip installed

## 8. PACKAGE MANAGEMENT

# Debian/Ubuntu (apt / dpkg)

* apt update — refresh package lists

* apt upgrade — upgrade installed packages

* apt install pkg — install package

* apt remove pkg — remove

* apt purge pkg — remove config files too

* dpkg -i package.deb — install .deb file

* dpkg -l | grep pkg — check package

# RHEL/CentOS/Fedora (yum/dnf/rpm)

* yum install pkg or dnf install pkg

* yum update or dnf upgrade

* rpm -ivh package.rpm — install rpm

* rpm -qa | grep pkg — list installed

* Arch (pacman)

* pacman -Syu — update system

* pacman -S pkg — install

Other

* snap install package  —(snap)

* flatpak  —commands

## 9. USERS & GROUPS

* useradd username — create user (use -m for home)

* adduser username — friendlier wrapper (Debian)

* userdel username — delete user

* usermod -aG group user — add user to group

* groups username — show groups

* passwd username — set/change password

* chage -l username — view password expiry

* sudo visudo — safely edit /etc/sudoers

* su - username — switch user (login shell)

## 10. PROCESSES & JOB CONTROL

* ps aux — show all processes

* ps -ef — alternate format

* top — dynamic process viewer

* htop — enhanced top (interactive)

* pgrep pattern — find PIDs

* pidof program — PID(s) of program

* kill PID — send SIGTERM (15)

* kill -9 PID — SIGKILL (9)

* kill -SIGINT PID — named signal

* pkill name — kill by name

* killall name — kill all processes by name

* nice -n 10 command — run with lower priority

* renice -n 5 -p PID — change priority of running process

* Job control in bash:

 * **command &** run in background
 
 * **jobs** list jobs
 
 * **fg %1** bring job 1 foreground
 
 * **bg %1** resume job in background
 
## 11. SYSTEMD & SERVICES

* systemctl status — overall status

* systemctl status <service> — service status

* systemctl start <service>

* systemctl stop <service>

* systemctl restart <service>

* systemctl reload <service> — reload config without restart

* systemctl enable <service> — start at boot

* systemctl disable <service>

* systemctl is-enabled <service>

* systemctl daemon-reload — after modifying unit files

* systemctl list-units --type=service — list services

* systemctl --failed — show failed units

* systemd-analyze blame — show boot time contributions

* Timers

 * systemctl list-timers — view systemd timers

## 12. NETWORKING

* ip addr / ip a — show interfaces & addresses

* ip link — show network links

* ip route — routing table

* ip neigh — ARP table

* ss -tuln — sockets listening (replacement for netstat)

* netstat -tulpn — network connections (if installed)

* ifconfig — older tool (deprecated)

* nmcli — NetworkManager CLI

 * nmcli device status

 * nmcli connection show

* ping host — test connectivity

* traceroute host — path to host

* tracepath host — user-mode traceroute

* dig domain — DNS lookup (from bind-utils)

* nslookup domain — DNS lookup (older)

* arp -a — ARP entries

* ethtool eth0 — show NIC settings

* ethtool -s eth0 speed 100 duplex full — change NIC (may require down)

* route — older route tool

# Firewall

* iptables -L -n -v — list iptables rules

* iptables -A INPUT -p tcp --dport 22 -j ACCEPT — add rule

* iptables-save / iptables-restore

* nft / nftables — modern replacement

* firewall-cmd --zone=public --add-port=8080/tcp --permanent (firewalld)

* ufw status / ufw allow 22 (Ubuntu uncomplicated firewall)

# SSH

* ssh user@host — connect

* ssh -p 2222 user@host — custom port

* ssh -i /path/key.pem user@host — use key

* ssh-keygen -t rsa -b 4096 -C "email@domain" — generate key

* ssh-copy-id -i ~/.ssh/id_rsa.pub user@host — copy key to remote

* scp file user@host:/path/ — secure copy

* sftp user@host — interactive file transfer

* rsync -avz source/ user@host:/dest/ — fast sync (recommended over scp for many files)

## 13. DISK, PARTITIONS & FILESYSTEMS

* df -h — disk free space (human)

* du -sh * — disk usage of dirs/files

* lsblk — list block devices

* fdisk -l — partition table

* parted /dev/sda — partition editor (scriptable)

* mkfs.ext4 /dev/sda1 — make ext4 filesystem

* mkfs.xfs /dev/sdb1 — make XFS filesystem

* mount /dev/sda1 /mnt — mount

* umount /mnt — unmount (note: umount, not unmount)

* /etc/fstab — persistent mounts at boot

* blkid — show filesystem UUIDs

* tune2fs -L label /dev/sda1 — label ext[2/3/4]

* fsck -f /dev/sda1 — filesystem check/repair (unmounted)

* resize2fs /dev/sda1 — resize ext filesystem

* losetup -fP disk.img — setup loop device

* mount -o loop disk.img /mnt — mount disk image

* dd if=/dev/zero of=file.img bs=1M count=100 — create sparse/blank image

* dd if=/dev/sda of=/backup/sda.img bs=4M conv=sync,noerror — disk cloning (careful)

# 14. LOGS & JOURNAL

* /var/log/ — system logs

  * /var/log/syslog or /var/log/messages — general system log

  * /var/log/auth.log — authentication (Debian)
  
  * /var/log/secure — authentication (RHEL)
  
  * /var/log/kern.log — kernel messages

* journalctl — systemd journal viewer

 * journalctl -u sshd.service — logs for unit
 
 * journalctl -b — logs from current boot
 
 * journalctl -f — follow
 
 * journalctl --since "2025-11-01" --until "2025-11-10"

## 15. BOOT & KERNEL

* dmesg — kernel ring buffer

* uname -r — kernel release

* grub2-mkconfig -o /boot/grub2/grub.cfg (RHEL/Fedora) or update-grub (Debian)

* grub-install /dev/sda — install grub to disk

* systemd-analyze blame / systemd-analyze plot > boot.svg

## 16. SECURITY: SUDO, SELINUX, APPARMOR
```
sudo command            # run command as root
sudo -i                 # open root shell
sudo -u user command    # run as another user
sudo visudo             # safely edit sudoers file

```

# SELinux (RHEL/CentOS/Fedora)
```
getenforce              # check mode (Enforcing/Permissive)
setenforce 0            # set permissive mode temporarily
sestatus                # detailed SELinux status
semanage port -l        # list allowed ports
semanage port -a -t http_port_t -p tcp 8081   # allow new port
restorecon -Rv /var/www # restore security contexts
audit2why -a            # explain access denials
audit2allow -a -M mypol # generate allow policy module

```
# AppArmor (Ubuntu)
```
aa-status               # show active profiles
aa-complain <prog>      # disable blocking, log only
aa-enforce <prog>       # enforce security
aa-disable <prog>       # disable profile

```
## 17. Bash Shell Basics & Scripting
-------------------------------

## 18. Networking Advanced Commands

# network inspection ()
```
ip a                  # show interfaces
ip route              # show routing table
ip neigh              # ARP table
hostnamectl          # hostname info

```
# testing connections
```
ping host
traceroute host
tracepath host
```

# Port/Traffic analysis
```
ss -tulnp             # show listening ports
netstat -tulnp        # older tool
tcpdump -i eth0       # capture packets
tcpdump -nn port 80   # capture HTTP traffic

```


# DNS tools
```
dig domain.com
nslookup domain.com
host domain.com
```
# File transfers
```
scp file user@host:/path/
rsync -avz /src/ /dest/
sftp user@host
```
# Curl / Wget
```
curl -I https://site.com          # headers
curl -O https://site.com/file     # download
curl -X POST -d "a=1&b=2" URL
wget -c URL                       # continue download
wget -r URL                       # recursive download

```
## 19. Troubleshooting & Debugging Tools
# Process & system inspection
```
ps aux
top
htop
free -h
df -h
vmstat 1
iostat -x 1
mpstat -P ALL 1
```

# Logs
```
dmesg -T
journalctl -xe
journalctl -u sshd
tail -f /var/log/syslog
```
# Network debugging
```
lsof -i :8080         # who is using port 8080
ss -lptn              # listening sockets
```
# Program debugging
```
strace command        # trace syscalls
strace -p <pid>       # attach to running program
ltrace command        # trace library calls
```
# File monitoring
```
watch -n 1 'df -h'
inotifywait -m /path
```
## 20. Advanced Filesystem Commands
# Disk usage
```
du -sh *              # size of files/folders
lsblk                 # block devices
blkid                 # filesystem UUIDs
```

# Mounting
```
mount /dev/sda1 /mnt
umount /mnt
mount -o loop disk.img /mnt
```

# Filesystem creation
```
mkfs.ext4 /dev/sda1
mkfs.xfs /dev/xvdf1
```

# Repair & check
```
fsck -f /dev/sda1
e2fsck -f /dev/sda1
badblocks -v /dev/sda1
```
# Resize filesystem
```
resize2fs /dev/sda1        # EXT
xfs_growfs /mountpoint     # XFS
```
# Freeze filesystem
```
fsfreeze -f /mount
fsfreeze -u /mount
```




