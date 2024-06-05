# sbc-networking
Exploration of the limits of networking on SBC


## Aims
1. Set up SBC Leader with shared network connection on USB to Ethernet adaptor (from CLI if possible)
2. Set up SBC Follower with DHCP connection on main ethernet port, and DHCP (for shared network) on USB to Ethernet adaptor
3. Use WebSoCat to send data packets in each direction over shared network connection
4. Power down both SBCs, and check network settings remain consistant on re-powering
5. Ensure that WebSoCat connection is able to be established & capable of sending & recieving data packets.

# Steps Taken
## step 1. Check for additional network adaptors:
https://www.baeldung.com/linux/list-network-cards

### Option 1: Use lshw command
 creates comprehensive summaries of the system’s hardware components. To do this, it mainly examines several files in the /proc directory. <br>
    `sudo lshw -C network`
The -C network option filters the output to show only the network cards along with their properties. This information includes the description, vendor, driver, capabilities, and others.
Also, we can use the -short option to see an overview and ensure that only network cards are shown

### Option 2: Using the /sys/class/net/ Directory
- Run the ls command against this directory, we should see all available network interfaces. This includes both physical and virtual devices.
-  `ls /sys/class/net/ `
- Use some filtering to identify only physical cards
- `find /sys/class/net -type l -not -lname '*virtual*' -printf '%f\n'`
- Let’s break down the above find command:
    -type l: looks for symbolic links
    -not -lname: ignores the path that contains the virtual string
    -printf ‘%f\n’: prints only the basename of the path

- use the name of the interface to get more information about it.
- For this, we navigate to the `cd /sys/class/net/` directory.
- Now, we go to the relevant device directory by name.
- Finally, we open the uevent file, which contains information about the interfaces, such as their MAC address, driver, and others.

For example, to get data about the eno1 interface, we can use a simple cat command:

`cat /sys/class/net/eno1/uevent`

Found this USB Ethernet Device:
`/sys/class/net/enxa0cec8a0f73c`

## step 2. set up adaptor as shared internet connection:

