Computer Hardware
<details>
<summary>CMOD Battery - Powers BIOS chip</summary>
<code style="white-space:wrap;">
BIOS Process
    - Performs Power-On-Self-Test
    - Loads OS files from hard disk to RAM
    - Boots up and connects hardware to OS

Failure of CMOS battery is indicated by constant beeping sounds and date&time reset

BIOS can be used to overclock the CPU
    - clock speed = reading rate of incoming electrical pulse
</code>
</details>
Internal Memory
    - ROM (stable memory): stores firmware files (hardware control)
    - RAM (volatile memory): allows to use multiple apps at the same time

CPU (silicon chip)
    - dual core (!= single_core x2) the 2nd process start a little before the first process finishes
    - server CPUs have about 70 cores
    - app data access pattern
        CPU registers <=> L1 cache <=> L2 cache <=> L3 cache <=> RAM <=> Hard disk

Transistor - controls the flow of the electrical signals
           - transistors can be combined to form a logic gate

RAID (Redundant Array of Independent Disks)
    - RAID 0: spread data accross multiple disks
    - RAID 1: keep a copy of each disk
    - RAID 5: use a parity disk (ie: Disk A XOR Disk B = Disk C)
        A and B are data disks and C is parity disk - XOR can be used to recover failure of any 1 disk - assuming it is unlikely 2 disks would fail simultaneously
    - RAID 10 = RAID 1 + 0 = spread data across different pairs of disks and each pair is copy of each other
