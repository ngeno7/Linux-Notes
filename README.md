## Linux Notes

![linux](https://user-images.githubusercontent.com/9430676/181217374-9419762c-d0d7-4ae7-989f-b2db52341ca7.png)
[<img src="[(https://user-images.githubusercontent.com/9430676/181217374-9419762c-d0d7-4ae7-989f-b2db52341ca7.png)" height="250"/>]([image.png](https://user-images.githubusercontent.com/9430676/181217374-9419762c-d0d7-4ae7-989f-b2db52341ca7.png))

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

  > logger [options] message (-p FACILITY.SERVERITY -t TAG)

LogRotate: - Compress, remove or mail log files.

## Disk management
- **Partitions:**
  - Allow you to separate data.
  - Can protect the whole system.
  -
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
    
#### TODO: Disk management
#### TODO: User and group management
## Networking
- **TCP/IP**
- **Classful networks**
    - A, B and C.
    - IP, subnet mask, Broadcast address.
- **Classless Inter-Domain Routing/CIDR**
- **Private Address Space**
- **Determining your IP Address
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
        - **traceroute** / **tracepath** shows the path a packet takes to the destination
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
        -  *-vvv* Even more verbose output.
