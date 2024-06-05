# sbc-networking
Exploration of the limits of networking on SBC



## Aims
1. Set up SBC Leader with shared network connection on USB to Ethernet adaptor (from CLI if possible)
2. Set up SBC Follower with DHCP connection on main ethernet port, and DHCP (for shared network) on USB to Ethernet adaptor
3. Use WebSoCat to send data packets in each direction over shared network connection
4. Power down both SBCs, and check network settings remain consistant on re-powering
5. Ensure that WebSoCat connection is able to be established & capable of sending & recieving data packets.
