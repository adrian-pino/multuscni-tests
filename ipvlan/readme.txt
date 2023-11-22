# Ping between pods works, but I don't know where is flowing the traffic.

# Running tcpdump in the master interface (ens3) doesn't show any traffic
# With macvlan I do see such traffic flowing from the ens3 interface...

# From one pod I can see the following:
k exec -it dnsutils-kubemaster -- sh
 
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: tunl0@NONE: <NOARP> mtu 1480 qdisc noop qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
4: eth0@if199: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1480 qdisc noqueue 
    link/ether 7e:b8:04:7f:06:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.141.14/32 scope global eth0
       valid_lft forever preferred_lft forever
5: net1@tunl0: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether fa:16:3e:7b:42:e6 brd ff:ff:ff:ff:ff:ff
    inet 172.16.10.130/24 brd 172.16.10.255 scope global net1
       valid_lft forever preferred_lft forever

/ # route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         169.254.1.1     0.0.0.0         UG    0      0        0 eth0
169.254.1.1     0.0.0.0         255.255.255.255 UH    0      0        0 eth0
172.16.10.0     0.0.0.0         255.255.255.0   U     0      0        0 net1

/ # arp -n
? (172.16.10.131) at fa:16:3e:7b:42:e6 [ether]  on net1
? (172.16.10.30) at ee:ee:ee:ee:ee:ee [ether]  on eth0
? (169.254.1.1) at ee:ee:ee:ee:ee:ee [ether]  on eth0

