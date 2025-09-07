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
