i would use becasue the VM acts like another computer on the same network, so my classmates computer can reach it.

I would not use NAT because NAT lets the VM get out to the network, but another computer can't normally start a connection directly to it without something like port forwarding.

The downside is that bridged puts the VM more directly on the physsical network, so you lose some of NAT's isolation.