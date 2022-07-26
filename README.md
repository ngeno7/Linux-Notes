[AWS Global Infrastructure1.pdf](https://github.com/ngeno7/Linux-Notes/files/9354565/AWS.Global.Infrastructure1.pdf)
## Linux Notes

### System Logs

Help us to know what is going on different processes, to assist in knowing the health of processes.
Syslog standard aids in processing of messages. Allows logging to be centrally controlled.
Logs are categorized according to:
  - Serverity
  - Facility
Selector Fields:
  - FACILITY.SERVERITY
Action Field:
 - Determine how the message is processed.

  >logger [options] message (-p FACILITY.SERVERITY -t TAG)
>LogRotate: - Compress, remove or mail log files.

---
## Disk management
- **Partitions:**
  - Allow you to separate data.
  - Can protect the whole system.
- **MBR: master boot record**; supports up to 2TB of storage.
  - It is the boot sector at the beginning of a storage device.
  - It is being phased out by GPT (GUID Partition Table)
  - allow upto 4 Primary partitions
  - Extended partitions allow you to create logical partitions.

- **GPT: GUID Partition Table - ( GUID: Global Unique Identifier )**
  - Replaces MBR partitioning system.
  - Part of UEFI (Unified Extensible Firmware Interface).
  - UEFI is replacing BIOS.
  - Supports up to 128 partitions.
  - support up to 9.4 ZB disk sizes.
  - not supported by older OS'es
  - May require newer or special tools

- **Mount Point:** Directory used to access data on a partition.
  - / (slash) is always a mounting point.

- **fdisk:** tool used for partitioning disks.
  Alternatives: gdisk, parted.
- **File Systems**:
   - *EXT (Extended File System)* was made specifically for linux.
   - e.g ext1, ext2, ext3 etc.
   - Others: ReiserFS, JFS, XFS, ZFS, Btrfs
   - Command: *mkfs -t TYPE DEVICE*
---
#### TODO: Disk management
---
#### TODO: User and group management
---
## Networking
- **TCP/IP**
- **Classful networks**
    - A, B and C.
    - IP, subnet mask, Broadcast address.
- **Classless Inter-Domain Routing/CIDR**
- **Private Address Space**
- Determining your IP Address
    - Command:
        - *ip address / ip a / ip address show / ip a s*
        - *ifconfig*
 - DNS Hostnames
    - DNS: to translate human-readable names into IP addresses
    - FQDN = Fully qualified domain name
    - TLD = Top level domain e.g .com, .net, .org
    - Resolve domain name using the: *host* and *dig* command
    
 - Network Ports
    - When a service starts it binds itself to a port.
        - Examples of ports: *1-1, 023* are well known ports.
            - *22 SSH, 25 SMTP, 80 HTTP, 143 IMAP, 389 LDAP, 443 HTTPS*.
 - DHCP
    - Dynamic Host Configuration Protocol
    - Assign IP to clients. IP Netmask, gateway, DNS Servers.

- Network Troubleshooting
    - Test For Connectivity using ping command
        - *ping HOST / ping -c COUNT HOST*
        - Ping tests the endpoint but does not show the route the packets take.
        - *traceroute -n google.com* 
        - *-n* option skips translating the ip to domain name
        - **traceroute** shows the path a packet takes to the destination
     - **netstat** used to display different network information
        -  *-n* numeric addresses and ports
        -  *-i* list of network interfaces
        -  *-r* the route table (netstat -rn)
        -  *-p* PID and program used
        -  *-l* listening sockets
        -  *-t* limit the output to TCP (netstat -ntlp)
        -  *-u* limit the output to UDP (netstat -nulp)
    - Packet sniffing with **tcpdump**
        - *tcpdump*
        -  *-n* display numeric addresses and ports
        -  *-A* display ASCII(text) output
        -  *-v* Verbose mode. produce more output
        -  *-vvv* Even more verbose output
---
## Advanced Linux Permissions
  - Special Modes
    - Setuid:
      - When a process is started, it runs using the starting user's UID and GID
      - setuid = Set User ID upon execution
      - programs that require include: ping , chsh
      - add setUID command: *chmod u+s FILE* / *chmod 4755 FILE*
      - Remove setUID command: *chmod u-s FILE* / *chmod 0755 FILE*
      - Find setuid files: *find / -perm /4000 -ls*

    - setgid:
      - setgid = Set Group ID upon execution
      - add setgid
        - *chmod ug+s FILE*
        - *chmod 6755 FILE*

       - Remove setgid
          - *chmod g-s FILE*
          - *chmod 0755 FILE*
      - Setgid on a directory causes new files to inherit the group of the directory
      - setgid causes  directories to inherit the setgid bit.
      - Is not retroactive
      - Great for working with groups.

    - Integrity checker
        - find
        - tripwire
        - AIDE (Advanced Intrusion Detection Environment)
        - OSSEC
        - Samhain
        - Package managers
    - The sticky bit
        - used on a directory to only allow the owner of the file/directory to delete it.
        - used on /tmp
        - Add command:
            - chmod o+t FILE
            - chmod 1777 FILE
        - Remove command:
            - chmod o-t FILE
            - chmod 0777 FILE

    - Reading the *ls* output
        - A capitalized special permission means the underlying permission is not set.
        - A lowercase special permission means the underlying normal permission is set.
--- 
 ## Command line tips
  - to use the last item on the command line use: '!$'
  - 
[AWS Global Infrastructure1.pdf](https://github.com/ngeno7/Linux-Notes/files/9354569/AWS.Global.Infrastructure1.pdf)

### First Bash 

```bash
#!/bin/bash

echo "Coping databases"
month=$(date +%b)
year=$(date +%Y)

if [ ! -d /root/website-backup/${year} ]
then
     echo "Creating ${year} folder..."
     mkdir /root/website-backup/${year}
fi
     echo "creating month folder..."
     if [ ! -d /root/website-backup/${year}/${month} ]
      then
        mkdir /root/website-backup/${year}/${month}
     fi
     echo "copying the backups from the server..."
     sshpass -p $1 scp root@[IP]:/root/testcopy.txt /root/website-backup/${year}/{month}
     #sshpass -p $1 scp -r root@[IP]:/mnt/sbs1/website/ /root/website-backup/${year}/{month}
     if [ $? == 0 ]
      then
         echo "Backups have been copied :)"
     else
         echo "Error occurred while backing up the data :("
     fi

```
