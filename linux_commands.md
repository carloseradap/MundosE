🔧 How Services Run

systemctl

Manage systemd services and targets.

systemctl status ssh         # Show SSH service status
systemctl start nginx        # Start nginx
systemctl stop nginx         # Stop nginx
systemctl restart nginx      # Restart nginx
systemctl enable nginx       # Enable nginx at boot
systemctl disable nginx      # Disable nginx at boot
systemctl list-units --type=service  # List active services

service

Legacy method to manage services (works on some distros).

service apache2 status       # Show apache2 service status
service nginx start          # Start nginx

journalctl

View system logs stored by systemd.

journalctl                   # View all logs
journalctl -xe               # Show recent logs with errors
journalctl -u nginx          # Logs for nginx service
journalctl -b -1             # Logs from previous boot

Targets (systemctl list-units --type=target)

Systemd targets are like runlevels.

systemctl get-default        # Get default target
systemctl list-units --type=target
systemctl isolate multi-user.target  # Switch to multi-user mode

🔐 How Permissions Work

chmod

Change file permissions.

chmod 755 script.sh          # rwxr-xr-x
chmod +x script.sh           # Add execute permission
chmod -R 644 myfolder        # Recursively set read/write permissions

chown

Change file ownership.

chown user:group file.txt    # Change owner and group
chown -R john:john /var/www  # Recursively change ownership

umask

Set default permissions for new files/directories.

umask                        # Show current value
umask 022                    # Default: 755 for dirs, 644 for files

Sticky Bit

Restricts file deletion in shared folders.

chmod +t /tmp
ls -ld /tmp                  # drwxrwxrwt

💽 How Storage Works

mount / umount

Manually mount or unmount devices.

mount /dev/sdb1 /mnt         # Mount device
umount /mnt                  # Unmount device

/etc/fstab

Used for automatic mounting on boot.

cat /etc/fstab               # View mount config

df

Display disk space usage.

df -h                        # Human-readable disk space

du

Display file or directory size.

du -sh /var/log              # Total size of /var/log
du -ah /var/log | sort -h    # List and sort by size

LVM (Logical Volume Manager)

pvdisplay                    # Physical volumes
vgdisplay                    # Volume groups
lvdisplay                    # Logical volumes

RAID Basics

cat /proc/mdstat             # View RAID status (mdadm based)

👤 How Users Are Managed

useradd, passwd

sudo useradd -m john         # Create user with home dir
sudo passwd john             # Set user password

groups, usermod

groups john                  # Show user's groups
usermod -aG sudo john        # Add to sudo group

/etc/sudoers (edit with visudo)

sudo visudo
# Add line: john ALL=(ALL) NOPASSWD:ALL

🐛 How to Debug Systems

Logs

less /var/log/syslog
less /var/log/messages

journalctl, ps, top

ps aux | grep nginx          # Check nginx process
ps -ef                       # Full-format listing
top                          # Real-time system usage

netstat / ss

netstat -tulnp               # Show open ports
ss -tuln                     # Faster, more modern

lsof

List open files by process or port.

lsof -i :80                  # Show who uses port 80
lsof /var/log/syslog         # Who is using a specific file

⚙️ How Linux Operates

Processes & Signals

ps aux                       # View processes
kill -9 <PID>                # Force kill
kill -SIGTERM <PID>          # Graceful kill

File System Navigation

ls -al /                     # Root directory structure
find /etc -name "*.conf"     # Search config files

systemd

systemctl                    # Manage system services

📈 How to Check Performance

top / htop

top                         # Real-time system monitor
htop                        # (if installed) Enhanced version

iostat, vmstat, sar, perf

iostat -xz 1               # CPU & disk I/O
vmstat 1                   # Memory and I/O
sar -u 1 3                 # CPU usage via sysstat
perf top                   # Real-time performance profiler

strace

Trace system calls.

strace -p <PID>             # Attach to process
strace ./script.sh          # Trace script execution

🌐 How Networking Works

Interfaces

ip a                        # List interfaces
ip link set eth0 up         # Enable interface

Ports and Services

ss -tuln                    # Listening ports

DNS

dig google.com              # DNS query
nslookup google.com         # Alternative DNS tool

Routing

ip route show               # Show routing table

Firewalls

sudo ufw status             # UFW firewall status
sudo iptables -L            # List iptables rules

🖥️ How to Use the Command Line

Basic Tools

grep 'root' /etc/passwd     # Search
awk -F: '{print $1}' /etc/passwd   # Print usernames
sed 's/bash/zsh/' /etc/passwd      # Replace text

Pipes and Redirects

cat file.txt | grep "hello" > result.txt  # Output to file

🤖 How to Write Automation Scripts

Bash Script

#!/bin/bash
echo "Hello, $USER"
date

Make it executable:

chmod +x script.sh
./script.sh

Cron Jobs

crontab -e                  # Edit user cron jobs

Example job: every day at 7 AM

0 7 * * * /home/user/backup.sh

Conditionals and Loops