<h1 style="color:#8096c2">Computer Hardware</h1>

<h3 style="color:#8096c2">CMOD Battery</h3> - Powers BIOS chip

<h3 style="color:#8096c2">BIOS Process</h3>
&ensp;&ensp;      - Performs Power-On-Self-Test <br>
&ensp;&ensp;      - Loads OS files from hard disk to RAM <br>
&ensp;&ensp;      - Boots up and connects hardware to OS <br> <br>

Failure of CMOS battery is indicated by constant beeping sounds and date&time reset <br> <br>

BIOS can be used to overclock the CPU <br>
&ensp;&ensp;      - **clock speed** = reading rate of incoming electrical pulse <br> <br>

<h3 style="color:#8096c2">Internal Memory</h3>

&ensp;&ensp;      - **ROM (stable memory)**: stores firmware files (hardware control) <br>
&ensp;&ensp;      - **RAM (volatile memory)**: allows to use multiple apps at the same time <br> <br>

<h3 style="color:#8096c2">CPU (silicon chip)</h3>
 &ensp;&ensp;     - dual core (!= single_core x2) the 2nd process start a little before the first process finishes <br>
 &ensp;&ensp;     - server CPUs have about 70 cores <br>
 &ensp;&ensp;     - app data access pattern <br>
 &ensp;&ensp;&ensp;    CPU registers <=> L1 cache <=> L2 cache <=> L3 cache <=> RAM <=> Hard disk <br> <br>

<h3 style="color:#8096c2">Transistor</h3> - controls the flow of the electrical signals <br>
&ensp;&ensp;           - transistors can be combined to form a logic gate <br> <br>

<h3 style="color:#8096c2">RAID (Redundant Array of Independent Disks)</h3>

- **RAID 0**: spread data accross multiple disks <br>
- **RAID 1**: keep a copy of each disk <br>
- **RAID 5**: use a parity disk (ie: Disk A XOR Disk B = Disk C) <br>
&ensp;&ensp;        unlikely for 2 disks to fail simultaneously <br>
- **RAID 10** = RAID 1 + 0 = spread data across different pairs of disks and each pair is copy of each other
 <br> <br>
 
____________________________________________________________________________


<h1 style="color:#8096c2">Bit Logic</h1>

<h3 style="color:#8096c2">Bit Manipulation</h3>
&ensp;&ensp;     bin# + bin# = bin# * 2 = logically left shift bin# by 1 bit <br>
&ensp;&ensp;     bin# * (2^x) = logically left shift bin# by x bits <br>

<h3 style="color:#8096c2">Bit Tricks</h3>

| XOR             |  and/or         |  and/or         |
|-----------------|-----------------|-----------------|
| x XOR 0 =  x    |    x or 0 = x   |    x and 1 = x  |
| x XOR 1 = ~x    |    x or x = x   |    x and x = x  |

<br> 

<h3 style="color:#8096c2">2's Complement and Negative Binary Numbers</h3>

- 1st way to write a negative binary number <br>
    - write 1 as the sign bit <br>
    - [In decimal] (2^the remaining # of bits excluding sign bit) + neg_num = y <br>
    - ans = write 1(sign-bit) and y in binary <br> <br>

- 2nd way to write a negative binary number <br>
    - write 1 as the sign bit <br>
    - neg_num * (-1) = j => write j in binary in the remaining # of bits (excluding sign bit) <br>
    - k = 1's complement of j (inverse each bit in j) + 1 <br>
    - ans = concatenate 1(sign-bit) and k <br>

<h3 style="color:#8096c2">Shifts</h3>

| Right                                                   |     Left                                                   |
| ------------------------------------                    |     ------------------------------------                   |
| **right rotate**: 1100 => 0110                          |    **left rotate**: 1100 => 1001                           |
| **right logical shift**: 1100 => 0->1100 => 0110        |    **left logically shift**: 1100 => 1100<-0 => 1000       |
| **right arithmetic shift**: 1100 => 1->1100 => 1110     |    **left arithmetic shift**: 1100 => 1100<-0 => 1000 <br>(same as left logical shift) |

<br> <br>

<h3 style="color:#8096c2">CPU Architecture</h3>

```
            [Control Unit, ALU, CPU Registers, L1 Cache]
                                 ^
                                 |
Input Devices =============>    RAM   ===============>  Output Devices
(ie: mouse, keyboard)            |                      (ie: monitor, speaker)
                                 v
                            [Hard Disk]
```
- **Control Unit Functions**
    - fetch (data from memory) <br>
    - decode (using binary decoder) <br>
    - execute <br>
    - write back to memory <br>











