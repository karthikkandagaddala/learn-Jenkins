**How to Install Jenkins**
34.234.82.152 | 172.31.24.166 | t3.micro | null
[ ec2-user@ip-172-31-24-166 ~ ]$ sudo su -

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 ~ ]# cd /etc/yum.repos.d/

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# vim jenkins.repo

[jenkins]
name=Jenkins-stable
baseurl=http://pkg.jenkins.io/redhat-stable
gpgcheck=1

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# yum install fontconfig java-21-openjdk

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# yum install jenkins

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# systemctl daemon-reload

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# systemctl enable jenkins
Created symlink /etc/systemd/system/multi-user.target.wants/jenkins.service → /usr/lib/systemd/system/jenkins.service.

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# systemctl start jenkins

34.234.82.152 | 172.31.24.166 | t3.micro | null
[ root@ip-172-31-24-166 /etc/yum.repos.d ]# systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server
     Loaded: loaded (/usr/lib/systemd/system/jenkins.service; enabled; preset: disabled)
     Active: active (running) since Sun 2025-09-07 16:31:25 UTC; 15s ago
   Main PID: 15092 (java)
      Tasks: 42 (limit: 4015)
     Memory: 386.8M
        CPU: 16.874s
     CGroup: /system.slice/jenkins.service
             └─15092 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080


**********************************************************************************
1. Grow the partition (if disk was resized in AWS/VM)
growpart /dev/nvme0n1 4

2. Resize the Physical Volume
pvresize /dev/nvme0n1p4

3. Extend the Logical Volume for /home
lvextend -l +100%FREE /dev/RootVG/homeVol

4. Grow the XFS Filesystem
xfs_growfs /home

5. Verify
df -h /home
lsblk

📌 Notes

If filesystem is ext4, replace step 4 with:

resize2fs /dev/RootVG/homeVol


These steps assume:

Disk = /dev/nvme0n1

Partition = nvme0n1p4

VG = RootVG

LV = homeVol

Mount = /home


**ALL This I did by ChatGPT.**
