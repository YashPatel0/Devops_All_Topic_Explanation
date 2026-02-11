# 🐧 Linux Commands for DevOps Engineers – Complete Cheat Sheet

> A practical and interview-focused Linux command reference for DevOps, Cloud, and System Engineers.

---

# 📌 Table of Contents

- Basic Navigation
- File & Directory Management
- File Viewing & Editing
- File Permissions & Ownership
- User & Group Management
- Process Management
- Disk, Memory & System Monitoring
- Networking Commands
- Search & Text Processing (Very Important)
- Package Management
- Service & Systemctl Commands
- Archiving & Compression
- Environment Variables
- Redirection & Pipes
- Cron Jobs & Background Jobs
- Log Monitoring
- Important Interview Commands

---

# 📁 1. Basic Navigation Commands

```bash
pwd                     # Print current directory
ls                      # List files
ls -la                  # List all files including hidden
ls -lh                  # Human-readable sizes
cd /path                # Change directory
cd ..                   # Move one directory back
clear                   # Clear terminal
history                 # Show command history
```

---

# 📂 2. File & Directory Management

```bash
mkdir dir               # Create directory
mkdir -p a/b/c          # Create nested directories
rmdir dir               # Remove empty directory
rm -r dir               # Remove directory
rm -rf dir              # Force remove directory (Use carefully ⚠)

touch file.txt          # Create empty file
cp file1 file2          # Copy file
cp -r dir1 dir2         # Copy directory
mv file newname         # Rename file
mv file /path           # Move file
```

---

# 📖 3. File Viewing & Editing

```bash
cat file.txt            # Display full file
less file.txt           # Scrollable view
head file.txt           # First 10 lines
head -n 50 file.txt     # First 50 lines
tail file.txt           # Last 10 lines
tail -f app.log         # Live log monitoring
nano file.txt           # Edit using nano
vi file.txt             # Edit using vi
```

---

# 🔐 4. File Permissions & Ownership

```bash
chmod 755 file.sh       # Set permission
chmod +x script.sh      # Make executable
chown user file         # Change owner
chown user:group file   # Change owner and group
```

### Permission Values

| Number | Permission |
|--------|------------|
| 4      | Read       |
| 2      | Write      |
| 1      | Execute    |

Example:

```bash
chmod 755 script.sh
```

---

# 👤 5. User & Group Management

```bash
whoami                      # Current user
id                          # User details
adduser devops              # Add user
userdel devops              # Delete user
groupadd docker             # Create group
usermod -aG docker user     # Add user to group
passwd user                 # Change password
```

---

# ⚙️ 6. Process Management

```bash
ps                          # Current processes
ps aux                      # All running processes
top                         # Live monitoring
htop                        # Advanced monitor (if installed)
kill PID                    # Kill process
kill -9 PID                 # Force kill
pkill nginx                 # Kill by process name
```

---

# 💾 7. Disk, Memory & System Monitoring

```bash
df -h                       # Disk usage
du -sh dir                  # Directory size
free -h                     # Memory usage
lsblk                       # Block devices
mount                       # Mounted filesystems
uptime                      # System uptime
uname -a                    # System info
hostnamectl                 # Host details
```

---

# 🌐 8. Networking Commands

```bash
ip a                        # Show IP address
ip r                        # Routing table
ping google.com             # Check connectivity
curl http://example.com     # Test API
wget URL                    # Download file
netstat -tulnp              # Open ports
ss -tulnp                   # Modern alternative
traceroute google.com       # Trace route
```

---

# 🔎 9. Search & Text Processing (🔥 Very Important for DevOps)

```bash
grep "error" file.log       # Search text
grep -i "error" file.log    # Case insensitive
grep -r "text" /var/log     # Recursive search

find / -name file.txt       # Find file
find / -type f -size +10M   # Files larger than 10MB

awk '{print $1}' file       # Print first column
sed 's/old/new/g' file      # Replace text globally
sort file                   # Sort lines
uniq file                   # Remove duplicates
wc -l file                  # Count lines
```

---

# 📦 10. Package Management

## Ubuntu / Debian

```bash
apt update
apt upgrade
apt install nginx
apt remove nginx
```

## RHEL / Amazon Linux / CentOS

```bash
yum install nginx
dnf install nginx
yum remove nginx
```

---

# 🔄 11. Service & Systemctl Commands

```bash
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl status nginx
systemctl enable nginx
systemctl disable nginx
```

Check service logs:

```bash
journalctl -u nginx
```

---

# 📦 12. Archiving & Compression

```bash
tar -cvf file.tar dir
tar -xvf file.tar
tar -czvf file.tar.gz dir
tar -xzvf file.tar.gz
zip file.zip file
unzip file.zip
```

---

# 🌱 13. Environment Variables

```bash
env
printenv
export VAR=value
echo $VAR
unset VAR
```

---

# 🔀 14. Redirection & Pipes

```bash
command > file          # Overwrite output
command >> file         # Append output
command < file          # Input redirection
command1 | command2     # Pipe output
2> error.log            # Redirect errors
```

---

# ⏰ 15. Cron Jobs & Background Jobs

```bash
crontab -l              # List cron jobs
crontab -e              # Edit cron jobs
nohup command &         # Run in background
jobs                    # Show background jobs
bg                      # Resume job in background
fg                      # Bring job to foreground
```

---

# 📜 16. Log Monitoring (Production Use)

```bash
tail -f /var/log/syslog
tail -f /var/log/messages
journalctl -xe
dmesg
```

---

# 🎯 17. Must-Know Commands for Interviews

- grep, awk, sed
- ps, top, kill
- chmod, chown
- df, du, free
- systemctl
- find
- curl
- crontab
- tar

---

# 🚀 Pro DevOps Tip

✔ Always use `-h` for human readable output  
✔ Use `tail -f` for debugging live logs  
✔ Combine `grep + tail` for real-time filtering  
✔ Understand permissions (755, 644) clearly  
✔ Practice log analysis in `/var/log`  

---

⭐ If this helped you, consider starring the repository!
