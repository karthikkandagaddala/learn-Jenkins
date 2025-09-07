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
52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# df -h

Filesystem                    Size  Used Avail Use% Mounted on
devtmpfs                      4.0M     0  4.0M   0% /dev
tmpfs                         881M     0  881M   0% /dev/shm
tmpfs                         353M  5.0M  348M   2% /run
/dev/mapper/RootVG-rootVol    6.0G  2.5G  3.6G  41% /
/dev/mapper/RootVG-homeVol    960M   40M  921M   5% /home
/dev/mapper/RootVG-varVol     2.0G  464M  1.5G  24% /var
/dev/mapper/RootVG-varTmpVol  2.0G   47M  1.9G   3% /var/tmp
/dev/mapper/RootVG-logVol     2.0G   66M  1.9G   4% /var/log
/dev/mapper/RootVG-auditVol   4.4G   64M  4.3G   2% /var/log/audit
/dev/xvda3                    424M  223M  202M  53% /boot
/dev/xvda2                    122M  7.0M  115M   6% /boot/efi
tmpfs                         177M     0  177M   0% /run/user/1001


52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# lsblk

NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
xvda                 202:0    0   40G  0 disk
├─xvda1              202:1    0    1M  0 part
├─xvda2              202:2    0  122M  0 part /boot/efi
├─xvda3              202:3    0  488M  0 part /boot
└─xvda4              202:4    0 19.4G  0 part
  ├─RootVG-rootVol   253:0    0    6G  0 lvm  /
  ├─RootVG-swapVol   253:1    0    2G  0 lvm  [SWAP]
  ├─RootVG-homeVol   253:2    0    1G  0 lvm  /home
  ├─RootVG-varVol    253:3    0    2G  0 lvm  /var
  ├─RootVG-varTmpVol 253:4    0    2G  0 lvm  /var/tmp
  ├─RootVG-logVol    253:5    0    2G  0 lvm  /var/log
  └─RootVG-auditVol  253:6    0  4.4G  0 lvm  /var/log/audit

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# growpart /dev/xvda 4

CHANGED: partition=4 start=1253376 old: size=40687616 end=41940991 new: size=82632671 end=83886046

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# pvresize /dev/xvda4

  Physical volume "/dev/xvda4" changed
  
  1 physical volume(s) resized or updated / 0 physical volume(s) not resized

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# lvextend -l +100%FREE /dev/RootVG/homeVol

  Size of logical volume RootVG/homeVol changed from 1.00 GiB (256 extents) to 21.00 GiB (5376 extents).
  
  Logical volume RootVG/homeVol successfully resized.

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# df -Th /home

Filesystem                 Type  Size  Used Avail Use% Mounted on

/dev/mapper/RootVG-homeVol xfs   960M   40M  921M   5% /home

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# xfs_growfs /home

meta-data=/dev/mapper/RootVG-homeVol isize=512    agcount=8, agsize=32768 blks

         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=1 inobtcount=1 nrext64=0
data     =                       bsize=4096   blocks=262144, imaxpct=25
         =                       sunit=1      swidth=1 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=16384, version=2
         =                       sectsz=512   sunit=1 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 262144 to 5505024

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# resize2fs /dev/RootVG/homeVol

resize2fs 1.46.5 (30-Dec-2021)

resize2fs: Bad magic number in super-block while trying to open /dev/RootVG/homeVol

Couldn't find valid filesystem superblock.

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# df -h /home lsblk

Filesystem                  Size  Used Avail Use% Mounted on
/dev/mapper/RootVG-homeVol   21G  192M   21G   1% /home
NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
xvda                 202:0    0   40G  0 disk
├─xvda1              202:1    0    1M  0 part
├─xvda2              202:2    0  122M  0 part /boot/efi
├─xvda3              202:3    0  488M  0 part /boot
└─xvda4              202:4    0 39.4G  0 part
  ├─RootVG-rootVol   253:0    0    6G  0 lvm  /
  ├─RootVG-swapVol   253:1    0    2G  0 lvm  [SWAP]
  ├─RootVG-homeVol   253:2    0   21G  0 lvm  /home
  ├─RootVG-varVol    253:3    0    2G  0 lvm  /var
  ├─RootVG-varTmpVol 253:4    0    2G  0 lvm  /var/tmp
  ├─RootVG-logVol    253:5    0    2G  0 lvm  /var/log
  └─RootVG-auditVol  253:6    0  4.4G  0 lvm  /var/log/audit

52.87.203.124 | 172.31.82.113 | t2.small | null

[ root@ip-172-31-82-113 /etc/yum.repos.d ]# df -h

Filesystem                    Size  Used Avail Use% Mounted on
devtmpfs                      4.0M     0  4.0M   0% /dev
tmpfs                         881M     0  881M   0% /dev/shm
tmpfs                         353M  5.0M  348M   2% /run
/dev/mapper/RootVG-rootVol    6.0G  2.5G  3.6G  41% /
/dev/mapper/RootVG-homeVol     21G  192M   21G   1% /home
/dev/mapper/RootVG-varVol     2.0G  464M  1.5G  24% /var
/dev/mapper/RootVG-varTmpVol  2.0G   47M  1.9G   3% /var/tmp
/dev/mapper/RootVG-logVol     2.0G   66M  1.9G   4% /var/log
/dev/mapper/RootVG-auditVol   4.4G   64M  4.3G   2% /var/log/audit
/dev/xvda3                    424M  223M  202M  53% /boot
/dev/xvda2                    122M  7.0M  115M   6% /boot/efi
tmpfs                         177M     0  177M   0% /run/user/1001

52.87.203.124 | 172.31.82.113 | t2.small | null

**ALL This I did by ChatGPT.**
