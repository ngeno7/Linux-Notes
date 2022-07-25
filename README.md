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

  > logger [options] message (-p FACILITY.SERVERITY -t TAG)

LogRotate: - Compress, remove or mail log files.

## Disk management
-Partitions:
  - Allow you to separate data.
  - Can protect the whole system.
  -
- MBR: master boot record; supports up to 2TB of storage.
  - It is the boot sector at the beginning of a storage device.
  - It is being phased out by GPT (GUID Partition Table)
  - 4 Primary partitions
  - Extended partitions allow you to create logical partitions.
  
