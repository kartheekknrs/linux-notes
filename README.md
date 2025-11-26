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

## 1️⃣ Basics & Environment

Linux basics help you understand the system identity, time, environment variables, and general info.
```
pwd                      # Shows the full path of the current working directory
whoami                   # Prints the logged-in username
hostname                 # System hostname
uname -a                 # Kernel name, version, architecture
date                     # Display system date and time
uptime                   # Shows uptime + load average (system load)
env                      # List all environment variables
export VAR=value         # Set an environment variable for current session
printenv VAR             # Display a specific environment variable
clear                    # Clear terminal screen
```
## 2️⃣ Filesystem Navigation & File Operations

Move around directories, create, modify and delete files/folders.

```
ls                       # List directory contents
ls -l                    # Long listing (permissions, owner, size)
ls -la                   # Include hidden files (starting with .)
cd /path                 # Change directory to the given path
cd ..                    # Go back one directory
mkdir folder             # Create a folder
mkdir -p a/b/c           # Create nested directories
touch file               # Create an empty file or update timestamp
cp src dest              # Copy file
cp -r dir1 dir2          # Copy directory recursively
mv old new               # Move or rename file/directory
rm file                  # Delete file
rm -rf folder            # Delete directory recursively (force)
ln -s target linkname    # Create a symbolic link
file filename            # Detect file type (binary/text/script)
```
## 3️⃣ File Viewing & Processing

Used for reading, paging, slicing, combining or manipulating text.
```
cat file                 # Print file contents
tac file                 # Print file in reverse order
less file                # View file with scroll option
head -n 20 file          # Show first 20 lines
tail -n 20 file          # Show last 20 lines
tail -f file             # Follow file changes (logs)
cut -d',' -f2 file       # Cut CSV file and show 2nd column
sort file                # Sort lines alphabetically
sort -n file             # Numeric sort
uniq file                # Remove duplicate lines
uniq -c file             # Count repeated lines
tr a-z A-Z < file        # Convert lowercase → uppercase
wc -l file               # Count number of lines
paste file1 file2        # Merge lines side-by-side
tee output.txt           # Save AND display output
```
## 4️⃣ Permissions & Ownership

Linux permissions manage who can read/write/execute a file.

# Permission basics:
```
r = read
w = write
x = execute
```
```
ls -l                     # Show permissions (rwxr-xr-x)
chmod 755 file            # Owner: rwx, group/others: rx
chmod u+rwx file          # Add permissions symbolically
chmod g-w file            # Remove write from group
chown user:group file     # Change file owner & group
chgrp group file          # Change group only
umask 022                 # Default file creation mask (removes write for group/others)
getfacl                   # Show ACL permissions
setfacl -m u:user:rw file # Add custom ACL for a user
```
## 5️⃣ Text Editing & Editors
```
Nano (easy editor)
nano file                # Open file
# Ctrl+O save, Ctrl+X exit, Ctrl+K cut, Ctrl+U paste
```
# Vim / Vi (powerful editor)
```
vim file                 # Open file in Vim
# i → insert mode
# Esc → exit insert mode
# :w → save
# :q → quit
# :wq → save & quit
# yy → copy line
# dd → delete line
# p  → paste
```
## 6️⃣ Searching (find / grep / locate)
```
grep → search inside files
grep "text" file          # Search for text
grep -i "text" file       # Case-insensitive
grep -n "text" file       # Show line numbers
grep -R "text" .          # Search recursively in directory
```

# find → search for files
```
find /path -name "*.log"               # Find log files
find . -type f -size +50M              # Files larger than 50MB
find . -mtime -2                       # Files modified in last 2 days
find . -name "*.tmp" -exec rm {} \;    # Delete matching files
```
# locate → fast file search
```
locate filename                        # Search from DB (very fast)
sudo updatedb                          # Update file database
```
## 7️⃣ Compression & Archiving
```
tar -cvf archive.tar dir/              # Create tar
tar -xvf archive.tar                   # Extract tar
tar -czvf archive.tar.gz dir/          # Create gzip tar
tar -xzvf archive.tar.gz               # Extract gzip tar
zip -r archive.zip dir/                # Zip folder
unzip archive.zip                      # Extract zip
gzip file                              # Compress file
gunzip file.gz                         # Extract gzip
```
## 8️⃣ Package Management

# APT (Ubuntu/Debian)
```sudo apt update
sudo apt upgrade
sudo apt install package
sudo apt remove package
dpkg -i file.deb
dpkg -l | grep name
```
# YUM / DNF (CentOS/RHEL/Fedora)
```
sudo yum install package
sudo dnf install package
sudo yum update
rpm -ivh file.rpm
rpm -qa | grep name
```
# Pacman (Arch Linux)
```
sudo pacman -S package
sudo pacman -Syu        # full update
```
# 9️⃣ Users & Groups
```
useradd username                 # add user
adduser username                 # friendlier version (Debian)
passwd username                  # set password
userdel username                 # delete user
usermod -aG group user           # add user to group
groups username                  # list groups
sudo visudo                      # edit sudo permissions safely
su - username                    # switch user
```
# 🔟 Processes & Job Control
```
ps aux                           # list all processes
ps -ef                           # alternative view
top                              # CPU/memory usage
htop                             # improved top (if installed)
kill PID                         # stop process
kill -9 PID                      # force kill
pkill processname                # kill by name

command &                        # run in background
jobs                             # list background jobs
fg %1                            # bring job to foreground
bg %1                            # resume job in background
```
## 1️⃣1️⃣ Systemctl & Services
```
systemctl status service         # service status
systemctl start service          # start
systemctl stop service           # stop
systemctl restart service        # restart
systemctl enable service         # start at boot
systemctl disable service        # disable at boot
systemctl daemon-reload          # reload systemd configs
systemctl --failed               # list failed units
```
## 1️⃣2️⃣ Networking
```
ip a                             # show active interfaces
ip route                         # routing table
ip neigh                         # ARP table
ss -tulnp                        # listening ports (modern)
netstat -tulnp                   # old alternative
ping host                        # test connectivity
traceroute host                  # show path
dig domain                       # DNS lookup
nslookup domain                  # alternative
```
# SSH, SCP, Rsync
```
ssh user@host                    # remote login
ssh -i key.pem user@host         # login with key
scp file user@host:/path/        # secure copy
rsync -avz src/ dest/            # efficient file sync
```

## 1️⃣3️⃣ Disk, Partitions & Filesystems
```df -h                            # disk usage
du -sh *                         # folder sizes
lsblk                            # list block devices
fdisk -l                         # partition info
mkfs.ext4 /dev/sda1              # create ext4 FS
mount /dev/sda1 /mnt             # mount filesystem
umount /mnt                      # unmount
blkid                            # show UUIDs
fsck -f /dev/sda1                # filesystem check
resize2fs /dev/sda1              # resize ext FS
xfs_growfs /mountpoint           # resize XFS
```
## 1️⃣4️⃣ Logs & Journal
```
ournalctl                      # system logs via journal
journalctl -u sshd              # service-specific logs
journalctl -f                   # follow logs (like tail -f)
journalctl --since "1 hour ago" # time-filtered logs
tail -f /var/log/syslog         # Debian/Ubuntu logs
tail -f /var/log/messages       # RHEL/CentOS logs
dmesg -T                        # kernel logs in readable format
```
## 1️⃣5️⃣ Boot & Kernel
```
uname -r                        # kernel version
dmesg                           # kernel ring buffer
systemd-analyze                 # boot-up performance
systemd-analyze blame           # which services slowed boot
update-grub (Debian/Ubuntu)     # update bootloader config
grub2-mkconfig -o /boot/grub2/grub.cfg   # RHEL/Fedora
reboot                          # restart system
poweroff                        # shutdown system
```
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




