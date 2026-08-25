
## **Basic Commands**

1. `pwd` – Print current working directory
2. `ls -l` – List files with details
3. `cd /path/to/dir` – Change directory
4. `mkdir new_folder` – Create a directory
5. `touch file.txt` – Create an empty file
6. `rm file.txt` – Delete a file
7. `rm -rf dir/` – Force delete a directory
8. `cp source.txt destination.txt` – Copy a file
9. `mv oldname.txt newname.txt` – Rename or move a file
10. `find /path -name "*.log"` – Find files by name
11. `locate filename` – Find a file (requires `updatedb`)
12. `stat file.txt` – Get file metadata
13. `df -h` – Show disk usage
14. `du -sh folder/` – Show folder size
15. `chmod 755 file.sh` – Change file permissions
16. `chown user:group file.txt` – Change file owner
17. `tar -cvf archive.tar folder/` – Create a tar archive
18. `tar -xvf archive.tar` – Extract a tar archive
19. `gzip file.txt` – Compress a file
20. `gunzip file.txt.gz` – Decompress a file

---

## **Networking Commands**

21. `ip a` – Show IP addresses
22. `hostname -I` – Get system IP
23. `ping google.com` – Check network connectivity
24. `curl -I https://example.com` – Get HTTP headers
25. `wget https://example.com/file.tar.gz` – Download a file
26. `scp user@remote:/file .` – Secure copy from remote server
27. `rsync -avz source/ dest/` – Efficient file sync
28. `netstat -tulnp` – List open ports
29. `ss -tulnp` – Alternative to netstat
30. `traceroute google.com` – Trace route to a host
31. `dig example.com` – Get DNS records
32. `nslookup example.com` – Query DNS
33. `ifconfig` – Show network interfaces (deprecated, use `ip a`)
34. `iptables -L` – Show firewall rules
35. `ufw status` – Check firewall status

---

## **Process & Performance Monitoring**

36. `ps aux` – List running processes
37. `top` – Monitor system resources
38. `htop` – Interactive process viewer
39. `kill -9 <PID>` – Force kill a process   || `kill -15 <PID>` – Graceful kill
40. `pkill -f processname` – Kill a process by name
41. `nohup command &` – Run a process in background
42. `nice -n 10 ./script.sh` – Set process priority
43. `renice -n 5 -p <PID>` – Change process priority
44. `strace -p <PID>` – Trace system calls
45. `lsof -i :8080` – Find process using a port

> Zombie Processes are those that have completed execution but still have an entry in the process table
> Sleeping Processes are those that are waiting for an event to occur
> Running Processes are those that are currently executing
> Stopped Processes are those that have been paused
> Idle Processes are those that are not doing anything
> Waiting Processes are those that are waiting for I/O operations
---

## **User & Group Management**

46. `whoami` – Show current user
47. `who` – List logged-in users
48. `w` – Show active users
49. `id` – Show user ID info
50. `adduser newuser` – Create a new user
51. `usermod -aG sudo username` – Grant sudo access
52. `passwd username` – Change user password
53. `groupadd devops` – Create a group
54. `usermod -aG devops username` – Add user to group
55. `groups username` – List user’s groups

---

## **File Processing & Text Manipulation**

56. `cat file.txt` – Show file contents
57. `tac file.txt` – Show file in reverse
58. `head -n 10 file.txt` – Show first 10 lines
59. `tail -n 10 file.txt` – Show last 10 lines
60. `tail -f logfile.log` – Continuously read log updates
61. `grep "error" logfile.log` – Search for a pattern
62. `awk '{print $2}' file.txt` – Extract column 2
63. `sed 's/foo/bar/g' file.txt` – Replace text
64. `cut -d':' -f1 /etc/passwd` – Extract fields
65. `sort file.txt` – Sort lines
66. `uniq file.txt` – Remove duplicate lines
67. `diff file1.txt file2.txt` – Compare files
68. `cmp file1.txt file2.txt` – Binary file comparison
69. `wc -l file.txt` – Count lines
70. `tee file.txt` – Write output to file & display

---

## **Disk & Storage Management**

71. `fdisk -l` – List disk partitions
72. `mkfs.ext4 /dev/sdb1` – Format disk partition
73. `mount /dev/sdb1 /mnt` – Mount a partition
74. `umount /mnt` – Unmount partition
75. `lsblk` – Show disk layout
76. `blkid` – Get UUID of partitions
77. `iostat` – Show disk I/O stats
78. `vmstat 1 5` – Monitor memory & CPU
> STORAGE Management
```bash
# Step 1: Create partition
sudo fdisk /dev/sdb
# Inside fdisk:
n   # new partition
p   # primary
1   # partition number
<Enter>  # default start sector
+10G     # size 10GB
w   # write changes

# Step 2: Format partition
sudo mkfs.ext4 /dev/sdb1

# Step 3: Create mount point
sudo mkdir /mnt/data1

# Step 4: Mount partition
sudo mount /dev/sdb1 /mnt/data1
```

---

## **Scheduling & Automation**

79. `crontab -e` – Edit crontab
80. `crontab -l` – List scheduled jobs
81. `at now + 5 minutes` – Schedule a one-time job
82. `systemctl list-timers` – List scheduled systemd timers

---

## **Package Management**

83. `apt update && apt upgrade` – Update packages (Debian/Ubuntu)
84. `yum update` – Update packages (RHEL/CentOS)
85. `dnf update` – Update packages (Fedora)
86. `apt install package` – Install a package
87. `apt remove package` – Remove a package
88. `apt autoremove` – Remove unused packages
89. `apt search package` – Search for a package
90. `apt show package` – Show package info
91. `apt list --installed` – List installed packages
92. `apt list --upgradable` – List upgradable packages
93. `apt-cache search package` – Search for a package in cache
94. `apt-cache show package` – Show package info from cache
95. `apt-cache policy package` – Show package policy
96. `apt-cache depends package` – Show package dependencies
97. `apt-cache rdepends package` – Show reverse dependencies
98. `apt-cache madison package` – Show package versions
99. `apt-cache showsrc package` – Show source package info
100. `apt-cache showpkg package` – Show package details
101. `apt-mark hold package` – Hold a package from updates
102. `apt-mark unhold package` – Unhold a package
---

## **DevOps & Cloud-Specific**

103. `docker ps` – List running containers
104. `docker images` – List Docker images
105. `docker run -d nginx` – Run a container
106. `kubectl get pods` – List Kubernetes pods
107. `kubectl logs podname` – Get pod logs
108. `kubectl exec -it podname -- /bin/bash` – Enter a running container
109. `terraform init` – Initialize Terraform
110. `terraform apply` – Apply Terraform configuration
111. `aws s3 ls` – List S3 buckets
112. `aws ec2 describe-instances` – List EC2 instances

---

## **Security & Logs**

113. `cat /var/log/syslog` – View system logs
114. `journalctl -u nginx` – View logs for a service
115. `fail2ban-client status` – Show failed login attempts
116. `auditctl -l` – List active audit rules
117. `passwd -l username` – Lock a user account
118. `history | grep sudo` – Find sudo history
119. `alias ll='ls -lah'` – Create a shortcut command
120. `unalias ll` – Remove alias

---

**🔥 Bonus Tip**:
Use **`man <command>`** to check any command’s manual! Example:

```bash
man grep
```
