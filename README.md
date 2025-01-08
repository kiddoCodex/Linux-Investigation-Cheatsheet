# Linux-Investigation-Cheatsheet
This cheatsheet includes common and powerful commands and tools for performing various Linux investigations. It covers monitoring, process management, user activity, logs, networking, system security, and more.


1. System Information

General System Info:

uname -a - Displays detailed kernel information
hostnamectl - Shows system hostname and related information
lsb_release -a - Provides Linux distribution details
cat /etc/os-release - Another way to display OS information
uptime - Shows system uptime and load average
top or htop - Real-time process viewer (htop is more interactive)
dmesg - Kernel ring buffer (hardware issues, startup logs)
free -h - Memory usage
df -h - Disk usage (free and used space)
lsblk - List block devices (partitions, disks)
lscpu - CPU architecture information
lspci - List PCI devices
lsusb - List USB devices

2. User Management & Authentication

Check User Information:

whoami - Current logged-in user
id - User ID and group ID information
cat /etc/passwd - List all users on the system
cat /etc/group - List all groups
groups <username> - List groups for a user
last - Show last logins
lastlog - Show last login for each user

Authentication Logs:

cat /var/log/auth.log - Authentication logs (login attempts, sudo usage)
journalctl -u ssh - Show SSH service logs
w - Who is logged in and what they are doing
who - Who is logged in (similar to w)
finger <username> - User information (if installed)

3. Process Monitoring

Process Information:

ps aux - List all running processes
top - Dynamic real-time process viewer
htop - Interactive process viewer (needs to be installed)
pgrep <pattern> - Find processes by name
pstree - View process tree
lsof - List open files and associated processes
pidof <process_name> - Find process ID (PID) of a running process
strace -p <pid> - Trace system calls of a process


System Resource Usage:

vmstat - System performance (process, memory, paging)
iostat - I/O statistics
mpstat - CPU performance (needs sysstat package)
sar - Collect and report system activity (needs sysstat package)
watch -n 1 'ps aux --sort=-%mem' - Monitor processes by memory usage in real-time

4. Networking

Networking Information:

ifconfig or ip a - Show IP addresses and network interfaces
ip link - View and manipulate network interfaces
ss -tuln - View listening TCP/UDP sockets
netstat -tuln - View listening ports (deprecated, use ss instead)
ss -s - Display socket statistics
nmap <host> - Network exploration tool (scan for open ports)
traceroute <host> - Trace the route packets take to a destination
ping <host> - Check network connectivity
dig <domain> - DNS lookup
nslookup <domain> - DNS query tool
route -n - View routing table
ip route - Show IP routing table
tcpdump -i eth0 - Capture network traffic on a specific interface

Firewall Configuration:

iptables -L - View firewall rules
ufw status - Check firewall status (for UFW users)
firewalld-cmd --list-all - Check firewalld rules

5. Logs and Log Analysis

System Logs:

cat /var/log/syslog - System log
cat /var/log/messages - System messages (depends on the distro)
cat /var/log/kern.log - Kernel logs
cat /var/log/dmesg - Boot messages (kernel messages)
journalctl - View logs managed by systemd
journalctl -u <service> - Logs for a specific systemd service

Log Analysis:

grep <pattern> <file> - Search logs for a specific pattern
logrotate - Manage log files (rotation, compression)
tail -f /var/log/auth.log - Monitor logs in real-time

6. File Integrity & Security

File Permission & Ownership:

ls -l <file> - View file permissions and ownership
chmod - Change file permissions
chown - Change file owner/group
stat <file> - Display file status (permissions, size, etc.)
Check for SUID/SGID Files:

find / -type f -perm /4000 - List files with the SUID bit
find / -type f -perm /2000 - List files with the SGID bit

Rootkits & Malware:

chkrootkit - Rootkit scanner
rkhunter --check - Rootkit hunter (needs installation)
lynis audit system - Security audit tool (needs installation)

File Integrity Checkers:

AIDE - File integrity checker (advanced)
tripwire - Intrusion detection system

7. Disk and File System Investigation

Disk Information:

fdisk -l - List all partitions
blkid - List block devices (partitions and UUIDs)
mount - View mounted file systems
lsblk - View block devices and their mount points
tune2fs -l /dev/sda1 - Display ext2/ext3/ext4 filesystem info
xfs_info /dev/sda1 - Display XFS filesystem info
smartctl -a /dev/sda - Display SMART disk health status

Disk Usage:

du -sh <dir> - Display disk usage of a directory
du -sh * - Display disk usage for files and subdirectories
find / -type f -size +100M - Find large files

File System Repair:

fsck - File system consistency check (use with caution, especially on mounted filesystems)

8. Cron Jobs and Schedules

Cron Jobs:

crontab -l - List cron jobs for the current user
crontab -e - Edit cron jobs
cat /etc/crontab - View system-wide cron jobs
ls -l /etc/cron.* - View cron job directories

at Jobs:

atq - List pending jobs scheduled with at
atrm <job_id> - Remove a specific job from the queue


9. Memory and Swap Investigation

Memory Usage:

free -h - Display memory usage
vmstat - System performance, including memory
htop - Interactive memory and CPU usage monitoring
ps aux --sort=-%mem - List processes by memory usage

Swap Usage:

swapon -s - View swap usage
free -h - Shows memory and swap in use

10. Package Management & Software Investigation

Installed Packages:

dpkg -l - List all installed packages (Debian-based)
rpm -qa - List all installed packages (Red Hat-based)
apt list --installed - List installed packages (Debian-based)
yum list installed - List installed packages (Red Hat-based)
snap list - List installed snap packages

Package Integrity:

debsums - Verify integrity of installed Debian packages
rpm -V <package_name> - Verify the integrity of a specific package (Red Hat-based)

Vulnerabilities:

apt-get update && apt-get upgrade - Update installed packages (Debian-based)
yum update - Update installed packages (Red Hat-based)
dnf update - Update installed packages (Fedora-based)

11. System Auditing

Audit Tools:

auditctl - Configure the audit system
ausearch - Search audit logs
auditd - Audit daemon for system monitoring

12. Backup and Recovery

Backup:

tar -cvf <archive_name>.tar <directory> - Backup a directory to a tarball
rsync -avz <source> <destination> - Sync directories/files over SSH

Recovery:

testdisk - Data recovery tool (CLI-based)
photorec - File recovery tool (CLI-based)

13. System Cleanup

Clean Cache:

apt-get clean - Remove downloaded package files (Debian-based)
yum clean all - Clean cache (Red Hat-based)
journalctl --vacuum-time=7d - Clean journal logs older than 7 days

Find Large Files:

find / -type f -size +500M - Find files larger than 500MB
