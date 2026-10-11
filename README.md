# HomeLab Documentation
My General Description for how I set up my homelab alongside with the sources that I utilized
This was started by me from the year 2022 and retired/completed in the year 2025 due to the 
difficulty of managing a server while pursuing my degree away from my home.

## TrueNAS Setup
1. Install TrueNAS Scale on your target system (with atleast 3 disks, one for TrueNAS install and other 2 for the portion to be accessed as a NAS) via official installation media and note down login details
2. Use a web browswer to access the webUI
3. Create a user with both read and write access to both access the data pool and to enable ACL
4. Create a storage pool and select the layout of the remaining 2 disks as mirrored (RAID1) or striped (RAID0) confirm its creation
5. Create the dataset, use the SMB/samba preset and confirm that the SMB service starts.
6. Access the permissions of the newly created dataset, add item and add a user/group, and set the permissions to both read and write in this case
7. Depending on the OS you use, check how to access SMB shares via the IP address of the target, enter the credentials of newly made user (username and password) and then a window should pop up in the file manager which is blank.
8. Upload files to your newly created NAS
### Additional info
1. Max data throughput is bottlenecked by the devices you use. Even using fast NVME SSDs to create a NAS, if the machine has only a 100 Mbps network card, you can only get a max upload/download speed of 100Mbps
2. Striping should never be utilized without parity for mission critical data. Striping increases performance at the cost of redundancy
### Sources
[Hardware Havens](https://www.youtube.com/@HardwareHaven)
[TrueNAS](https://www.truenas.com/)
