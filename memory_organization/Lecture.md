# Memory basics
A memory unit is a collection of storage units or devices together. The memory unit stores the binary information in the form of bits. Generally, memory/storage is classified into two categories:

- **Volatile Memory**: This loses its data, when power is switched off.
- **Non-Volatile Memory**: This permanent storage does not lose data when power is switched off.

<img width="619" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/d9b28d0f-8377-4194-85cf-75eca9d1809b">

The hierarchy of components can visualize the total memory capacity of a computer. The memory hierarchy system consists of all storage devices in a computer system, from the slow Auxiliary Memory to the fast Main Memory and smaller Cache memory.

**Auxillary memory** access time is generally **1000 times** that of the main memory. Hence it is at the bottom of the hierarchy.

The **main memory** occupies the central position because it is equipped to communicate directly with the CPU and with auxiliary memory devices through the Input/output processor (I/O).

When the program not residing in the main memory is needed by the CPU, they are brought in from auxiliary memory. Programs not currently required in main memory are transferred into auxiliary memory to provide space in main memory for other currently used programs.

The **cache memory** is used to store program data that is currently being executed in the CPU. The approximate access time ratio between cache memory and main memory is about **1 to 7~10**

Each memory type is a collection of numerous memory locations. To access data from any memory, first, it must be located, and then the data is read from the memory location. The following are the methods to access information from memory locations:

1. **Random Access**: Main memories are random access memories, with each memory location having a unique address. Using this unique address, any memory location can be reached in the same amount of time in any order.
2. **Sequential Access**: This method allows memory access in a sequence or in order.
3. **Direct Access**: In this mode, information is stored in tracks, each having a separate read/write head.

The memory unit communicating directly within the CPU, Auxiliary, and Cache memory is called main memory. It is the central storage unit of the computer system. It is a large and fast memory used to store data during computer operations. Main memory comprises **RAM** and **ROM**, with RAM-integrated circuit chips holding a significant share.

- RAM: Random Access Memory
  - **DRAM**: Dynamic RAM comprises capacitors and transistors and must be refreshed every 10~100 ms. It is slower and cheaper than SRAM.
  - **SRAM**: Static RAM has a six-transistor circuit in each cell and retains data until powered off.
  - **NVRAM**: Non-Volatile RAM retains its data, even when turned off—for example, Flash memory.
- ROM: Read Only Memory is non-volatile and more like permanent information storage. It also stores the **bootstrap loader** program to load and start the operating system when the computer is turned on. **PROM**(Programmable ROM), **EPROM**(Erasable PROM), and **EEPROM**(Electrically Erasable PROM) are some commonly used ROMs.

Devices that provide backup storage are called auxiliary memory. **For example, Magnetic disks and tapes are commonly used auxiliary devices. Other devices used as auxiliary memory are magnetic drums, magnetic bubble memory, and optical disks.

It is not directly accessible to the CPU, and is accessed using the Input/Output channels.

The data or contents of the main memory used repeatedly by the CPU are stored in the cache memory so that we can easily access that data in a shorter time.

Whenever the CPU needs to access memory, it first checks the cache memory. If the data is not found in cache memory, the CPU moves onto the main memory. It also transfers blocks of recent data into the cache and deletes the old data in the cache to accommodate the new one.

The performance of cache memory is measured in terms of a quantity called **hit ratio**. When the CPU refers to memory and finds the word in the cache, it is said to produce a **hit**. If the word is not found in the cache, it is in the main memory, then it counts as a **miss**.

The ratio of the number of hits to the total CPU references to memory is called the hit ratio. $Hit Ratio = Hit/(Hit + Miss)$.

It is also known as **content addressable memory (CAM)**. It is a memory chip in which each bit position can be compared. The content is compared in each bit cell, allowing speedy table lookup. Since the entire chip can be compared, contents are randomly stored without considering the addressing scheme. These chips have less storage capacity than regular memory chips.

From the earliest days of computing, programmers have wanted unlimited amounts of fast memory. The topics covered in the lecture aid programmers by creating that illusion. Before we look at creating the illusion, let's consider a simple analogy that illustrates the key principles and mechanisms that we use.

Suppose you were a student writing a term paper on important historical developments in computer hardware. You are sitting at a desk in a library with a collection of books that you have pulled from the shelves and are examining. You find that several of the important computers that you need to write about are described in the books you have, but there is nothing about the EDSAC. Therefore, you go back to the shelves and look for an additional book. You find a book on early British computers that covers the EDSAC. Once you have a good selection of books on the desk in front of you, there is a good probability that many of the topics you need can be found in them, and you may spend most of your time just using the books on the desk without going back to the shelves. Having several books on the desk in front of you saves time compared to having only one book there and constantly having to go back to the shelves to return it and take out another.

The same principle allows us to create the illusion of a large memory that we can access as fast as a very small memory. Just as you did not need to access all the books in the library at once with equal probability, a program does not access all of its code or data at once with equal probability. Otherwise, it would be impossible to make most memory accesses fast and still have large memory in computers, just as it would be impossible for you to fit all the library books on your desk and still find what you wanted quickly.

This underlies both the way in which you did your work in the library and the way that programs operate. The principle of locality states that programs access a relatively small portion of their address space at any instant of time, just as you accessed a very small portion of the library's collection. There are two different types of locality:

- *Temporal locality* (locality in time): if an item is referenced, it will tend to be referenced again soon. If you recently brought a book to your desk to look at, you will probably need to look at it again soon.
- *Spatial locality* (locality in space): if an item is referenced, items whose addresses are close by will tend to be referenced soon. For example, when you brought out the book on early English computers to find out about the EDSAC, you also noticed that there was another book shelved next to it about early mechanical computers, so you also brought back that book and, later on, found something useful in that book. Libraries put books on the same topic together on the same shelves to increase spatial locality. We'll see how memory hierarchies use spatial locality a little later in this chapter.

**Temporal locality**: The locality principle stating that if a data location is referenced then it will tend to be referenced again soon.

**Spatial locality**: The locality principle stating that if a data location is referenced, data locations with nearby addresses will tend to be referenced soon.

Just as accesses to books on the desk naturally exhibit locality, locality in programs arises from simple and natural program structures. For example, most programs contain loops, so instructions and data are likely to be accessed repeatedly, showing high amounts of temporal locality. Since instructions are normally accessed sequentially, programs also show high spatial locality. Accesses to data also exhibit a natural spatial locality. For example, sequential accesses to elements of an array or a record will naturally have high degrees of spatial locality.

We take advantage of the principle of locality by implementing the memory of a computer as a *memory hierarchy*. A memory hierarchy consists of multiple levels of memory with different speeds and sizes. The faster memories are more expensive per bit than the slower memories and thus are smaller.

By implementing the memory system as a hierarchy, the user has the illusion of a memory that is as large as the largest level of the hierarchy, but can be accessed as if it were all built from the fastest memory. Flash memory has replaced disks in many personal mobile devices, and may lead to a new level in the storage hierarchy for desktop and server computers.

<img width="549" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/02ebf98f-50b1-45e4-b351-b0db917632ac">

The data is similarly hierarchical: a level closer to the processor is generally a subset of any level further away, and all the data is stored at the lowest level. By analogy, the books on your desk form a subset of the library you are working in, which is in turn a subset of all the libraries on campus. Furthermore, as we move away from the processor, the levels take progressively longer to access, just as we might encounter in a hierarchy of campus libraries.

A memory hierarchy can consist of multiple levels, but data is copied between only two adjacent levels at a time, so we can focus our attention on just two levels. The upper level—the one closer to the processor—is smaller and faster than the lower level, since the upper level uses technology that is more expensive. The figure below shows that the minimum unit of information that can be either present or not present in the two-level hierarchy is called a *block* or a *line*; in our library analogy, a block of information is one book.

**Block (or line)**: The minimum unit of information that can be either present or not present in a cache.

<img width="305" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/36895b86-bf6a-47f9-9e21-3c1f38f7f76d">

1. A memory hierarchy can consist of multiple levels. The upper level—the one closer to the processor—is smaller and faster than the lower level.
2. Within each level, the unit of information that is present or not is called a block or a line.
3. Usually we transfer an entire block when we copy something between levels.

If the data requested by the processor appears in some block in the upper level, this is called a *hit* (analogous to your finding the information in one of the books on your desk). If the data is not found in the upper level, the request is called a *miss*. The lower level in the hierarchy is then accessed to retrieve the block containing the requested data. (Continuing our analogy, you go from your desk to the shelves to find the desired book.) The *hit rate*, or *hit ratio*, is the fraction of memory accesses found in the upper level; it is often used as a measure of the performance of the memory hierarchy. The *miss rate* (1 - hit rate) is the fraction of memory accesses not found in the upper level.

**Hit rate**: The fraction of memory accesses found in a level of the memory hierarchy.

**Miss rate**: The fraction of memory accesses not found in a level of the memory hierarchy.

Since performance is the major reason for having a memory hierarchy, the time to service hits and misses is important. *Hit time* is the time to access the upper level of the memory hierarchy, which includes the time needed to determine whether the access is a hit or a miss (that is, the time needed to look through the books on the desk). The *miss penalty* is the time to replace a block in the upper level with the corresponding block from the lower level, plus the time to deliver this block to the processor (or the time to get another book from the shelves and place it on the desk). Because the upper level is smaller and built using faster memory parts, the hit time will be much smaller than the time to access the next level in the hierarchy, which is the major component of the miss penalty. (The time to examine the books on the desk is much smaller than the time to get up and get a new book from the shelves.)

**Hit time**: The time required to access a level of the memory hierarchy, including the time needed to determine whether the access is a hit or a miss.

**Miss penalty**: The time required to fetch a block into a level of the memory hierarchy from the lower level, including the time to access the block, transmit it from one level to the other, insert it in the level that experienced the miss, and then pass the block to the requestor.

As we will, the concepts used to build memory systems affect many other aspects of a computer, including how the operating system manages memory and I/O, how compilers generate code, and even how applications use the computer. Of course, because all programs spend much of their time accessing memory, the memory system is necessarily a major factor in determining performance. The reliance on memory hierarchies to achieve performance has meant that programmers, who are trained to think of memory as a flat, random access storage device, need to understand that memory is a hierarchy to get good performance. 

Since memory systems are critical to performance, computer designers devote a great deal of attention to these systems and develop sophisticated mechanisms for improving the performance of the memory system. We will discuss the major conceptual ideas, although we use many simplifications and abstractions to keep the material manageable in length and complexity.

> Programs exhibit both temporal locality, the tendency to reuse recently accessed data items, and spatial locality, the tendency to reference data items that are close to other recently accessed items. Memory hierarchies take advantage of temporal locality by keeping more recently accessed data items closer to the processor. Memory hierarchies take advantage of spatial locality by moving blocks consisting of multiple contiguous words in memory to upper levels of the hierarchy.
>
> The figure below shows that a memory hierarchy uses smaller and faster memory technologies close to the processor. Thus, accesses that hit in the highest level of the hierarchy can be processed quickly. Accesses that miss go to lower levels of the hierarchy, which are larger but slower. If the hit rate is high enough, the memory hierarchy has an effective access time close to that of the highest (and fastest) level and a size equal to that of the lowest (and largest) level.
>
> In most systems, the memory is a true hierarchy, meaning that data cannot be present in level *i* unless it is also present in level *i* + 1.

<img width="490" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/d1b63217-407f-4b00-b692-23d72e5eb536">

This structure, with the appropriate operating mechanisms, allows the processor to have an access time that is determined primarily by level 1 of the hierarchy and yet have a memory as large as level *n*. Although the local disk is normally the bottom of the hierarchy, some systems use tape or a file server over a local area network as the next levels of the hierarchy.

## Memory technologies

There are four primary technologies used today in memory hierarchies. Main memory is implemented from DRAM (*dynamic random access memory*), while levels closer to the processor (caches) use SRAM (*static random access memory*). DRAM is less costly per bit than SRAM, although it is substantially slower. The price difference arises because DRAM uses significantly less area per bit of memory, and DRAMs thus have larger capacity for the same amount of silicon; the speed difference arises from several factors. The third technology is flash memory. This nonvolatile memory is the secondary memory in Personal Mobile Devices. The fourth technology, used to implement the largest and slowest level in the hierarchy in servers, is magnetic disk. The access time and price per bit vary widely among these technologies, as the table below shows, using typical values for 2020:

<img width="628" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/21e212a5-8926-47f0-9a82-d53520e510e6">

<img width="632" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/b490c057-566f-430a-8a66-75c74eae256b">

1. Memory systems are implemented as a hierarchy.
2. Closer memory levels are implemented with faster technologies, while lower memory levels are implemented with slower technologies with larger capacity.
3. Data requested by the processor similarly moves between levels.

### SRAM technology

SRAMs are simply integrated circuits that are memory arrays with (usually) a single access port that can provide either a read or a write. SRAMs have a fixed access time to any datum, though the read and write access times may differ.

SRAMs don't need to refresh and so the access time is very close to the cycle time. SRAMs typically use six to eight transistors per bit to prevent the information from being disturbed when read. SRAM needs only minimal power to retain the charge in standby mode.

In the past, most PCs and server systems used separate SRAM chips for either their primary, secondary, or even tertiary caches. Today, thanks to Moore's Law, all levels of caches are integrated onto the processor chip, so the market for separate SRAM chips has nearly evaporated.

### DRAM technology

In a SRAM, as long as power is applied, the value can be kept indefinitely. In a dynamic RAM (DRAM), the value kept in a cell is stored as a charge in a capacitor. A single transistor is then used to access this stored charge, either to read the value or to overwrite the charge stored there. Because DRAMs use only a single transistor per bit of storage, they are much denser and cheaper per bit than SRAM. As DRAMs store the charge on a capacitor, it cannot be kept indefinitely and must periodically be refreshed. That is why this memory structure is called dynamic, as opposed to the static storage in an SRAM cell.

To refresh the cell, we merely read its contents and write it back. The charge can be kept for several milliseconds. If every bit had to be read out of the DRAM and then written back individually, we would constantly be refreshing the DRAM, leaving no time for accessing it. Fortunately, DRAMs use a two-level decoding structure, and this allows us to refresh an entire *row* (which shares a word line) with a read cycle followed immediately by a write cycle.

<img width="595" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/b35dd85e-400b-4e53-86e6-739c07422c9c">

1. Modern DRAMs are organized in banks, typically four for DDR4.
2. Each bank consists of a series of rows. Sending a PRE (precharge) command opens or closes a bank.
3. A row address is sent with an Act (activate), which causes the row to transfer to a buffer.
4. When the row is in the buffer, it can be transferred by successive column addresses at whatever the width of the DRAM is (typically 4, 8, or 16 bits in DDR4) or by specifying a block transfer and the starting address.
5. Each command, as well as block transfers, is synchronized with a clock.

The improvements in access time have been slower but continuous, and cost roughly tracks density improvements, although cost is often affected by other issues, such as availability and demand. The cost per gibibyte is not adjusted for inflation. Price source is https://jcmit.net/memoryprice.htm

<img width="740" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/a4abbb02-b15e-40be-bf69-7757c35bbd90">

The row organization that helps with refresh also helps with performance. To improve performance, DRAMs buffer rows for repeated access. The buffer acts like an SRAM; by changing the address, random bits can be accessed in the buffer until the next row access. This capability improves the access time significantly, since the access time to bits in the row is much lower. Making the chip wider also improves the memory bandwidth of the chip. When the row is in the buffer, it can be transferred by successive addresses at whatever the width of the DRAM is (typically 4, 8, or 16 bits), or by specifying a block transfer and the starting address within the buffer.

To further improve the interface to processors, DRAMs added clocks and are properly called synchronous DRAMs or SDRAMs. The advantage of SDRAMs is that the use of a clock eliminates the time for the memory and processor to synchronize. The speed advantage of synchronous DRAMs comes from the ability to transfer the bits in the burst without having to specify additional address bits. Instead, the clock transfers the successive bits in a burst. The fastest version is called *Double Data Rate* (*DDR*) SDRAM. The name means data transfers on both the rising *and* falling edge of the clock, thereby getting twice as much bandwidth as you might expect based on the clock rate and the data width. The latest version of this technology is called DDR4. A DDR4-3200 DRAM can do 3200 million transfers per second, which means it has a 1600-MHz clock.

Sustaining that much bandwidth requires clever organization *inside* the DRAM. Instead of just a faster row buffer, the DRAM can be internally organized to read or write from multiple *banks*, with each having its own row buffer. Sending an address to several banks permits them all to read or write simultaneously. For example, with four banks, there is just one access time and then accesses rotate between the four banks to supply four times the bandwidth. This rotating access scheme is called *address interleaving*.

Although personal mobile devices like the iPad use individual DRAMs, memory for servers is commonly sold on small boards called *dual inline memory modules* (DIMMs). DIMMs typically contain 4-16 DRAMs, and they are normally organized to be 8 bytes wide for server systems. A DIMM using DDR4-3200 SDRAMs could transfer at 8 × 3200 = 25,600 megabytes per second. Such DIMMs are named after their bandwidth: PC25600. Since a DIMM can have so many DRAM chips that only a portion of them are used for a particular transfer, we need a term to refer to the subset of chips in a DIMM that share common address lines. To avoid confusion with the internal DRAM names of row and banks, we use the term *memory rank* for such a subset of chips in a DIMM.

SRAM is faster than DRAM, but DRAM is denser and cheaper. SRAM is thus typically used by processors for small fast on-chip cache, while DRAM is used for the larger main memory off-chip. Also, processors and SRAM are made using different chip design processes than DRAM, so putting DRAM on-chip with a processor is rare.

<img width="626" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/6a68ae52-b0d6-476e-890b-b6cdf73a0fc8">

1. SRAM read/writes are about 10x faster than for DRAM.
2. But DRAM's are about 5x denser (using only 1 transistor/cell). Because of the density and mass production, DRAM's are about 100x cheaper too.
3. Thus, SRAM is used primarily for a processor's small but fast cache or other small on-chip memory, while DRAM is used for a processor's large main memory off-chip.
4. 
### Flash memory

**Flash memory** is a type of *electrically erasable programmable read-only memory* (EEPROM).

Unlike disks and DRAM, but like other EEPROM technologies, writes can wear out flash memory bits. To cope with such limits, most flash products include a controller to spread the writes by remapping blocks that have been written many times to less trodden blocks. This technique is called *wear leveling*. With wear leveling, personal mobile devices are very unlikely to exceed the write limits in the flash. Such wear leveling lowers the potential performance of flash, but it is needed unless higher-level software monitors block wear. Flash controllers that perform wear leveling can also improve yield by mapping out memory cells that were manufactured incorrectly.

### Disk memory

As the figure below shows, a magnetic hard disk consists of a collection of platters, which rotate on a spindle at 5400 to 15,000 revolutions per minute. The metal platters are covered with magnetic recording material on both sides, similar to the material found on a cassette or videotape. To read and write information on a hard disk, a movable *arm* containing a small electromagnetic coil called a *read-write head* is located just above each surface. The entire drive is permanently sealed to control the environment inside the drive, which, in turn, allows the disk heads to be much closer to the drive surface. The diameter of today's disks is 2.5 or 3.5 inches, and there are typically one or two platters per drive today.

Each disk surface is divided into concentric circles, called *tracks*. There are typically tens of thousands of tracks per surface. Each track is in turn divided into *sectors* that contain the information; each track may have thousands of sectors. Sectors are typically 512 to 4096 bytes in size. The sequence recorded on the magnetic media is a sector number, a gap, the information for that sector including error correction code, a gap, the sector number of the next sector, and so on.

**Track**: One of thousands of concentric circles that make up the surface of a magnetic disk.

**Sector**: One of the segments that make up a track on a magnetic disk; a sector is the smallest amount of information that is read or written on a disk.

The disk heads for each surface are connected together and move in conjunction, so that every head is over the same track of every surface. The term *cylinder* is used to refer to all the tracks under the heads at a given point on all surfaces.

To access data, the operating system must direct the disk through a three-stage process. The first step is to position the head over the proper track. This operation is called a *seek*, and the time to move the head to the desired track is called the seek time.

**Seek**: The process of positioning a read/write head over the proper track on a disk.

Disk manufacturers report minimum seek time, maximum seek time, and average seek time in their manuals. The first two are easy to measure, but the average is open to wide interpretation because it depends on the seek distance. The industry calculates average seek time as the sum of the time for all possible seeks divided by the number of possible seeks. Average seek times are usually advertised as 3 ms to 13 ms, but, depending on the application and scheduling of disk requests, the actual average seek time may be only 25% to 33% of the advertised number because of locality of disk references. This locality arises both because of successive accesses to the same file and because the operating system tries to schedule such accesses together.

Once the head has reached the correct track, we must wait for the desired sector to rotate under the read/write head. This time is called the *rotational latency* or *rotational delay*. The average latency to the desired information is halfway around the disk. Disks rotate at 5400 RPM to 15,000 RPM. The average rotational latency at 5400 RPM is

<img width="677" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/af3684d8-2ce8-46ee-b2a1-a68569be079d">

**Rotational latency**: Also called **rotational delay**. The time required for the desired sector of a disk to rotate under the read/write head; usually assumed to be half the rotation time.

The last component of a disk access, *transfer time*, is the time to transfer a block of bits. The transfer time is a function of the sector size, the rotation speed, and the recording density of a track. Transfer rates in 2020 were between 150 and 250 MB/sec.

One complication is that most disk controllers have a built-in cache that stores sectors as they are passed over; transfer rates from the cache are typically higher, and were up to 1500 MB/sec (12 Gbit/sec) in 2020.

The assumptions of the sector-track-cylinder model above are that nearby blocks are on the same track, blocks in the same cylinder take less time to access since there is no seek time, and some tracks are closer than others. The reason for the change was the raising of the level of the disk interfaces. To speed-up sequential transfers, these higher-level interfaces organize disks more like tapes than like random access devices. The logical blocks are ordered in serpentine fashion across a single surface, trying to capture all the sectors that are recorded at the same bit density to try to get best performance. Hence, sequential blocks may be on different tracks.

In summary, the two primary differences between magnetic disks and semiconductor memory technologies are that disks have a slower access time because they are mechanical devices—flash latency is 1000 times as fast and DRAM is 100,000 times as fast—yet they are cheaper per bit because they have very high storage capacity at a modest cost—disks are 6 to 300 times cheaper. Magnetic disks are nonvolatile like flash, but unlike flash there is no write wear-out problem. However, flash is much more rugged and hence a better match to the jostling inherent in personal mobile devices.

## Cache memory

In our library example, the desk acted as a cache—a safe place to store things (books) that we needed to examine. *Cache* was the name chosen to represent the level of the memory hierarchy between the processor and main memory in the first commercial computer to have this extra level. Today, although this remains the dominant use of the word *cache*, the term is also used to refer to any storage managed to take advantage of locality of access. Caches first appeared in research computers in the early 1960s and in production computers later in that same decade; every general-purpose computer built today from servers to low-power embedded processors, includes caches.

In this section, we begin by looking at a very simple cache in which the processor requests are each one word and the blocks also consist of a single word. The figure below shows such a simple cache, before and after requesting a data item that is not initially in the cache. Before the request, the cache contains a collection of recent references $X_1 , X_2 , …, X_{n-1}$ , and the processor requests a word $X_n$ that is not in the cache. This request results in a miss, and the word $X_n$ is brought from memory into the cache.

<img width="390" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/7e5c5111-adb2-4b15-ba4d-74acdcf70389">

This reference causes a miss that forces the cache to fetch $X_n$ from memory and insert it into the cache.

**Direct-mapped cache**: A cache structure in which each memory location is mapped to exactly one location in the cache.

If the number of entries in the cache is a power of 2, then modulo can be computed simply by using the low-order $log_2$ (cache size in blocks) bits of the address. Thus, an 8-block cache uses the three lowest bits (8 = $2^3$) of the block address. For example, the figure below shows how the memory addresses between $1_{10}$ $(00001_2)$ and $29_{10}$ $(11101_2)$ map to locations $1_{10}$ $(001_{2}$) and $5_{10}$ $(101_2)$ in a direct-mapped cache of eight words.

<img width="723" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/55281c9b-4534-4f14-9763-7242932f6c6f">

1. Because there are eight words in the cache, an address X maps to the direct-mapped cache word X modulo 8.
2. If the number of entries is a power of 2, then modulo can be computed simply by using the low-order log_2 (cache size in blocks) bits of the address.
3. Each cache location can contain the contents of a number of different memory locations. Addresses 00001_2, 01001_2, 10001_2, and 11001_2 all map to entry 001_2 of the cache.
4. Addresses 00101_2, 01101_2, 10101_2, and 11101_2 all map to entry 101_2 of the cache.

Because each cache location can contain the contents of a number of different memory locations, how do we know whether the data in the cache corresponds to a requested word? That is, how do we know whether a requested word is in the cache or not? We answer this question by adding a set of *tags* to the cache. The tags contain the address information required to identify whether a word in the cache corresponds to the requested word. The tag needs only to contain the upper portion of the address, corresponding to the bits that are not used as an index into the cache. For example, in the above figure we need only have the upper 2 of the 5 address bits in the tag, since the lower 3-bit index field of the address selects the block. Architects omit the index bits because they are redundant, since by definition the index field of any address of a cache block must be that block number.

**Tag**: A field in a table used for a memory hierarchy that contains the address information required to identify whether the associated block in the hierarchy corresponds to a requested word.

We also need a way to recognize that a cache block does not have valid information. For instance, when a processor starts up, the cache does not have good data, and the tag fields will be meaningless. Even after executing many instructions, some of the cache entries may still be empty. Thus, we need to know that the tag should be ignored for such entries. The most common method is to add a *valid bit* to indicate whether an entry contains a valid address. If the bit is not set, there cannot be a match for this block.

**Valid bit**: A field in the tables of a memory hierarchy that indicates that the associated block in the hierarchy contains valid data.

<img width="710" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/e9f8b919-ad88-4202-8e09-cf8eb4ddf647">
<img width="703" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/8c3a8f0b-95e6-4ab5-b673-c5b76141473b">
<img width="738" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/c590ffb4-0bc3-4fad-9056-08a4780a6aba">
<img width="705" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/449d9edf-2ae8-4f15-8006-854b45f29fac">
<img width="674" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/f796cef0-07d8-44ca-9fb6-af1254bfffa8">
<img width="700" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/b0a490e8-f3fb-49cf-bf46-24f413952936">

1. The three lowest bits of the memory reference are used to determine which cache block the memory reference is mapped to.
2. The corresponding tag is compared to the upper 2 bits of the memory reference to determine if the word in the cache corresponds to the requested word.
3. The valid bit indicates that the cache entry contains valid information. A cache hit occurs if the valid bit is set and the tag matches the upper bits of the memory reference.
4. A cache miss occurs if the requested word is not in the cache.
5. Upon a miss, the requested word is fetched from memory and inserted into the cache.
6. A cache miss also occurs if the cache block does not contain valid data, which would also result in fetching the requested word from memory.

In general, handling reads is a little simpler than handling writes, since reads do not have to change the contents of the cache. After seeing the basics of how reads work and how cache misses can be handled, we'll examine the cache designs for real computers and detail how these caches handle writes.

> Caching is perhaps the most important example of the big idea of **prediction**. It relies on the principle of locality to try to find the desired data in the higher levels of the memory hierarchy, and provides mechanisms to ensure that when the prediction is wrong it finds and uses the proper data from the lower levels of the memory hierarchy. The hit rates of the cache prediction on modern computers are often higher than 95%.

We know where to look in the cache for each possible address: the low-order bits of an address can be used to find the unique cache entry to which the address could map. The figure below shows how a referenced address is divided into

- A *tag field*, which is used to compare with the value of the tag field of the cache
- A *cache index*, which is used to select the block

This cache holds 1024 words or 4 KiB. We assume 32-bit addresses in this chapter. The tag from the cache is compared against the upper portion of the address to determine whether the entry in the cache corresponds to the requested address. Because the cache has 210 (or 1024) words and a block size of one word, 10 bits are used to index the cache, leaving 32 - 10 - 2 = 20 bits to be compared against the tag. If the tag and upper 20 bits of the address are equal and the valid bit is on, then the request hits in the cache, and the word is supplied to the processor. Otherwise, a miss occurs.

<img width="540" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/ded663fb-97ec-4c3b-a407-f65bf3faa307">

Larger blocks exploit spatial locality to lower miss rates. As the figure below shows, increasing the block size usually decreases the miss rate. The miss rate may go up eventually if the block size becomes a significant fraction of the cache size, because the number of blocks that can be held in the cache will become small, and there will be a great deal of competition for those blocks. As a result, a block will be bumped out of the cache before many of its words are accessed. Stated alternatively, spatial locality among the words in a block decreases with a very large block; consequently, the benefits in the miss rate become smaller.

Note that the miss rate actually goes up if the block size is too large relative to the cache size. Each line represents a cache of different size. (This figure is independent of associativity, discussed soon.)

<img width="614" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/e71275bf-db36-49db-9010-6dee77a87833">

A more serious problem associated with just increasing the block size is that the cost of a miss increases. The miss penalty is determined by the time required to fetch the block from the next lower level of the hierarchy and load it into the cache. The time to fetch the block has two parts: the latency to the first word and the transfer time for the rest of the block. Clearly, unless we change the memory system, the transfer time—and hence the miss penalty—will likely increase as the block size increases. Furthermore, the improvement in the miss rate starts to decrease as the blocks become larger. The result is that the increase in the miss penalty overwhelms the decrease in the miss rate for blocks that are too large, and cache performance thus decreases. Of course, if we design the memory to transfer larger blocks more efficiently, we can increase the block size and obtain further improvements in cache performance. 

### Handling cache misses

Before we look at the cache of a real system, let's see how the control unit deals with *cache misses*. The control unit must detect a miss and process the miss by fetching the requested data from memory (or, as we shall see, a lower-level cache). If the cache reports a hit, the computer continues using the data as if nothing happened.

**Cache miss**: A request for data from the cache that cannot be filled because the data is not present in the cache.

Modifying the control of a processor to handle a hit is trivial; misses, however, require some extra work. The cache miss handling is done in collaboration with the processor control unit and with a separate controller that initiates the memory access and refills the cache. The processing of a cache miss creates a pipeline stall as opposed to an interrupt, which would require saving the state of all registers. For a cache miss, we can stall the entire processor, essentially freezing the contents of the temporary and programmer-visible registers, while we wait for memory. More sophisticated out-of-order processors can allow execution of instructions while waiting for a cache miss.

Let's look a little more closely at how instruction misses are handled; the same approach can be easily extended to handle data misses. If an instruction access results in a miss, then the content of the Instruction register is invalid. To get the proper instruction into the cache, we must be able to instruct the lower level in the memory hierarchy to perform a read. Since the program counter is incremented in the first clock cycle of execution, the address of the instruction that generates an instruction cache miss is equal to the value of the program counter minus 4. Once we have the address, we need to instruct the main memory to perform a read. We wait for the memory to respond (since the access will take multiple clock cycles), and then write the words containing the desired instruction into the cache.

We can now define the steps to be taken on an instruction cache miss:

1. Send the original PC value (current PC - 4) to the memory.
2. Instruct main memory to perform a read and wait for the memory to complete its access.
3. Write the cache entry, putting the data from memory in the data portion of the entry, writing the upper bits of the address (from the ALU) into the tag field, and turning the valid bit on if it was not on already.
4. Restart the instruction execution at the first step, which will refetch the instruction, this time finding it in the cache.

The control of the cache on a data access is essentially identical: on a miss, we simply stall the processor until the memory responds with the data.

### Handling writes

Writes work somewhat differently. Suppose on a store instruction, we wrote the data into only the data cache (without changing main memory); then, after the write into the cache, memory would have a different value from that in the cache. In such a case, the cache and memory are said to be inconsistent. The simplest way to keep the main memory and the cache consistent is always to write the data into both the memory and the cache. This scheme is called *write-through*.

**Write-through**: A scheme in which writes always update both the cache and the next lower level of the memory hierarchy, ensuring that data is always consistent between the two.

The other key aspect of writes is what occurs on a write miss. We first fetch the words of the block from memory. After the block is fetched and placed into the cache, we can overwrite the word that caused the miss into the cache block. We also write the word to main memory using the full address.

Although this design handles writes very simply, it would not provide very good performance. With a write-through scheme, every write causes the data to be written to main memory. These writes will take a long time, likely at least 100 processor clock cycles, and could slow down the processor considerably. For example, suppose 10% of the instructions are stores. If the CPI without cache misses was 1.0, spending 100 extra cycles on every write would lead to a CPI of 1.0 + 100 × 10% = 11, reducing performance by more than a factor of 10.

One solution to this problem is to use a *write buffer*. A write buffer stores the data while it is waiting to be written to memory. After writing the data into the cache and into the write buffer, the processor can continue execution. When a write to main memory completes, the entry in the write buffer is freed. If the write buffer is full when the processor reaches a write, the processor must stall until there is an empty position in the write buffer. Of course, if the rate at which the memory can complete writes is less than the rate at which the processor is generating writes, no amount of buffering can help, because writes are being generated faster than the memory system can accept them.

**Write buffer**: A queue that holds data while the data is waiting to be written to memory.

The rate at which writes are generated may also be less than the rate at which the memory can accept them, and yet stalls may still occur. This can happen when the writes occur in bursts. To reduce the occurrence of such stalls, processors usually increase the depth of the write buffer beyond a single entry.

The alternative to a write-through scheme is a scheme called *write-back*. In a write-back scheme, when a write occurs, the new value is written only to the block in the cache. The modified block is written to the lower level of the hierarchy when it is replaced. Write-back schemes can improve performance, especially when processors can generate writes as fast or faster than the writes can be handled by main memory; a write-back scheme is, however, more complex to implement than write-through.

**Write-back**: A scheme that handles writes by updating values only to the block in the cache, then writing the modified block to the lower level of the hierarchy when the block is replaced.

## Summary

We began the previous section by examining the simplest of caches: a direct-mapped cache with a one-word block. In such a cache, both hits and misses are simple, since a word can go in exactly one location and there is a separate tag for every word. To keep the cache and memory consistent, a write-through scheme can be used, so that every write into the cache also causes memory to be updated. The alternative to write-through is a write-back scheme that copies a block back to memory when it is replaced.

To take advantage of spatial locality, a cache must have a block size larger than one word. The use of a larger block decreases the miss rate and improves the efficiency of the cache hardware by reducing the amount of tag storage relative to the amount of data storage in the cache. Although a larger block size decreases the miss rate, it can also increase the miss penalty. If the miss penalty increased linearly with the block size, larger blocks could easily lead to lower performance.

To avoid performance loss, the bandwidth of main memory is increased to transfer cache blocks more efficiently. Common methods for increasing bandwidth external to the DRAM are making the memory wider and interleaving. DRAM designers have steadily improved the interface between the processor and memory to increase the bandwidth of burst mode transfers to reduce the cost of larger cache block sizes.
