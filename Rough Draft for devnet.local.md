```
===================================================================================
                        VIRTUALBOX ISOLATED NETWORK LAB
                           Domain: devnet.local
                         Subnet: 192.168.1.0 /24 (255.255.255.0)
===================================================================================

              +-------------------------------------------------------+
              |                 VIRTUALBOX HYPERVISOR                 |
              |                    (CachyOS Host)                     |
              +-------------------------------------------------------+
                                          |
          +-------------------------------+-------------------------------+
          |                               |                               |
          v                               v                               v
+-------------------------+  +-------------------------+  +-------------------------+
|   debian.devnet.local   |  |    win11.devnet.local   |  |    winxp.devnet.local   |
|   (Debian 13 Server)    |  |  (Windows 11 / Tiny11)  |  |    (Windows XP SP3)     |
+-------------------------+  +-------------------------+  +-------------------------+
| IP:   192.168.1.10      |  | IP:   192.168.1.11      |  | IP:   192.168.1.12      |
| Role: Infrastructure    |  | Role: Admin Workstation |  | Role: Legacy Endpoint   |
+-------------------------+  +-------------------------+  +-------------------------+
| TOTAL VDI SIZE: 25 GB   |  | TOTAL VDI SIZE: 30 GB   |  | TOTAL VDI SIZE: 15 GB   |
|                         |  |                         |  |                         |
| PARTITION LAYOUT:       |  | PARTITION LAYOUT:       |  | PARTITION LAYOUT:       |
|  [sda1] /boot/efi       |  |  [Partition 1] System   |  |  [C: Drive] Primary     |
|   -> Size: 512 MB       |  |   -> Size: 100 MB       |  |   -> Size: 15 GB        |
|   -> Format: FAT32      |  |   -> Format: FAT32 (EFI)|  |   -> Format: NTFS       |
|                         |  |                         |  |                         |
|  [sda2] / (Root)        |  |  [C: Drive] Windows     |  | *(Note: Entire disk     |
|   -> Size: 22.5 GB      |  |   -> Size: 29.3 GB      |  |   allocated as a        |
|   -> Format: EXT4       |  |   -> Format: NTFS       |  |   single partition)*    |
|                         |  |                         |  |                         |
|  [sda3] swap            |  |  [Partition 3] Recovery |  |                         |
|   -> Size: 2.0 GB       |  |   -> Size: 600 MB       |  |                         |
|   -> Format: SWAP       |  |   -> Format: NTFS       |  |                         |
+-------------------------+  +-------------------------+  +-------------------------+
        | NIC:                          | NIC:                     | NIC:
        | [devnet.local]                | [devnet.local]           | [devnet.local]
        +-------------------------------+--------------------------+
                                        |
                                        v
                        +-----------------------------------+
                        |   VirtualBox Switch Environment   |
                        |   Internal Name: [devnet.local]   |
                        +-----------------------------------+
