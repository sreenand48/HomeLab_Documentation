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
- [Hardware Havens](https://www.youtube.com/@HardwareHaven)
- [TrueNAS](https://www.truenas.com/)

## Pi-Hole Setup
1. Install one of the recommended operating systems on your target server (I used debian linux in my case)
2. Pin the IP address of the target server using the configuration of your router
3. Start the installation command ```bash curl -sSL https://install.pi-hole.net | bash ``` on the target system
4. Enable the admin interface and note down the username and pasword
5. After the process is done, use a separate machine to log-in via the web interface
6. After confirming the web interface works, open a new tab to any website with ads
7. Confirm you are being shown advertisements, and for now, change your DNS server to the newly made Pi-Hole server
8. On refreshing the page, all the ads should dissapear. You ca also check the web interface for the amount of requests blocked
9. To set the configuration network wide, change the default/No. 1 DNS server of the router to the Pi-Hole Server and the secondary to the default ISP provided DNS server.

### Sources
- [Pi-Hole Docs](https://docs.pi-hole.net/main/basic-install/)
- [Debian](https://www.debian.org/)

## Netbootxyz Setup
1. Install any supported linux distro on your netboot server with dnsmasq
2. Configure dnsmasq by setting ```bash dhcp-option=66,"0.0.0.0" ``` and configure tftp using ```bash enable-tftp
tftp-root=/var/lib/tftp
dhcp-boot=netboot.xyz.kpxe ```
3. Run the docker installation of the netbootxyz server image
4. On the router settings, pin the IP address of the netboot server and also pin the DHCP server responsibility to the server.
5. Go to the web interface for the netbootxyz docker image and download the OS images you are most likely to use
6. Configure the boot.cfg settings change the live_endpoint to your server's IP
7. After that, plug in your target device via an ethernet cable to your router and boot it up selecting the NIC as an option
8. It will boot up with a netbootxyz page, from which you can select which OS you want to load. It will copy the OS image to ram via the ethernet cable

### Sources
- [netbootxyz](https://netboot.xyz/)
- [Archwiki Dnsmasq page](https://wiki.archlinux.org/title/Dnsmasq#DHCP_server)
  
