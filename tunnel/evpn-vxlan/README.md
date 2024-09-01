# evpn-vxlan

## 動作確認

### \[vyos01\] show bgp l2vpn evpn summary

```txt
vyos@vyos01:~$ show bgp l2vpn evpn summary
BGP router identifier 10.1.1.1, local AS number 65001 vrf-id 0
BGP table version 0
RIB entries 11, using 1056 bytes of memory
Peers 1, using 20 KiB of memory

Neighbor        V         AS   MsgRcvd   MsgSent   TblVer  InQ OutQ  Up/Down State/PfxRcd   PfxSnt Desc
10.2.2.2        4      65002       293       295        9    0    0 00:37:19            3        8 N/A

Total number of neighbors 1
```

### \[vyos01\] show bgp l2vpn evpn neighbors 10.2.2.2 advertised-routes

```txt
vyos@vyos01:~$ show bgp l2vpn evpn neighbors 10.2.2.2 advertised-routes
BGP table version is 0, local router ID is 10.1.1.1
Default local pref 100, local AS 65001
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          Next Hop            Metric LocPrf Weight Path
Route Distinguisher: 10.1.1.1:2
 *> [2]:[0]:[48]:[aa:c1:ab:ba:87:d6]
                                       32768 i
 *> [2]:[0]:[48]:[aa:c1:ab:ba:87:d6]:[128]:[fe80::a8c1:abff:feba:87d6]
                                       32768 i
 *> [3]:[0]:[32]:[10.1.1.1]
                                       32768 i
Route Distinguisher: 10.1.1.1:3
 *> [2]:[0]:[48]:[aa:c1:ab:ba:87:d6]
                                       32768 i
 *> [2]:[0]:[48]:[aa:c1:ab:ba:87:d6]:[128]:[fe80::a8c1:abff:feba:87d6]
                                       32768 i
 *> [3]:[0]:[32]:[10.1.1.1]
                                       32768 i
Route Distinguisher: 10.1.1.1:4
 *> [3]:[0]:[32]:[10.1.1.1]
                                       32768 i
Route Distinguisher: 10.3.3.3:2
 *> [2]:[0]:[48]:[aa:c1:ab:78:86:d4]
                                           0 65002 65003 i
 *> [2]:[0]:[48]:[aa:c1:ab:78:86:d4]:[128]:[fe80::a8c1:abff:fe78:86d4]
                                           0 65002 65003 i
 *> [3]:[0]:[32]:[10.3.3.3]
                                           0 65002 65003 i
Route Distinguisher: 10.3.3.3:3
 *> [3]:[0]:[32]:[10.3.3.3]
                                           0 65002 65003 i
Route Distinguisher: 10.3.3.3:4
 *> [3]:[0]:[32]:[10.3.3.3]
                                           0 65002 65003 i

Total number of prefixes 12
```

### \[\vyos01\] show evpn mac vni all

```txt
vyos@vyos01:~$ show evpn mac vni all
VNI 10000 #MACs (local and remote) 2

Flags: N=sync-neighs, I=local-inactive, P=peer-active, X=peer-proxy
MAC               Type   Flags Intf/Remote ES/VTEP            VLAN  Seq #'s
aa:c1:ab:78:86:d4 remote       10.3.3.3                             1/0
aa:c1:ab:ba:87:d6 local        eth1                                 0/0

VNI 10200 #MACs (local and remote) 2

Flags: N=sync-neighs, I=local-inactive, P=peer-active, X=peer-proxy
MAC               Type   Flags Intf/Remote ES/VTEP            VLAN  Seq #'s
aa:c1:ab:78:86:d4 remote       10.3.3.3                             0/0
aa:c1:ab:ba:87:d6 local        eth1.200                             0/0

VNI 10100 #MACs (local and remote) 2

Flags: N=sync-neighs, I=local-inactive, P=peer-active, X=peer-proxy
MAC               Type   Flags Intf/Remote ES/VTEP            VLAN  Seq #'s
aa:c1:ab:78:86:d4 remote       10.3.3.3                             0/0
aa:c1:ab:ba:87:d6 local        eth1.100                             0/0
```

### \[vyos01\] show tech-support report

<details><summary>show tech-support report</summary>

`````txt
vyos@vyos01:~$ sh tech-support report

---

## VyOS Version and Package Changes

Version: VyOS 1.5-rolling-202407300021
Release train: current
Release flavor: generic

Built by: autobuild@vyos.net
Built on: Tue 30 Jul 2024 02:54 UTC
Build UUID: 34639626-cff6-4000-b1a2-ea261788fd3b
Build commit ID: bf3c5d3ac25f11

Architecture: x86_64
Boot via: installed image
System type: QEMU guest

Hardware vendor: QEMU
Hardware model: Standard PC (Q35 + ICH9, 2009)
Hardware S/N:
Hardware UUID: Unknown

Copyright: VyOS maintainers and contributors

---

## Configuration file

interfaces {
loopback lo {
}
}
service {
ntp {
allow-client {
address "127.0.0.0/8"
address "169.254.0.0/16"
address "10.0.0.0/8"
address "172.16.0.0/12"
address "192.168.0.0/16"
address "::1/128"
address "fe80::/10"
address "fc00::/7"
}
server time1.vyos.net {
}
server time2.vyos.net {
}
server time3.vyos.net {
}
}
}
system {
config-management {
commit-revisions "100"
}
console {
device ttyS0 {
speed "115200"
}
}
host-name "vyos"
login {
user vyos {
authentication {
encrypted-password "$6$QxPS.uk6mfo$9QBSo8u1FkH16gMyAVhus6fU3LOzvLR9Z9.82m3tiHFAxTtIkhaZSWssSgzt4v4dGAL8rhVQxTg0oAG9/q11h/"
plaintext-password ""
}
}
}
syslog {
global {
facility all {
level "info"
}
facility local7 {
level "debug"
}
}
}
}

// Warning: Do not remove the following line.
// vyos-config-version: "bgp@5:broadcast-relay@1:cluster@2:config-management@1:conntrack@5:conntrack-sync@2:container@2:dhcp-relay@2:dhcp-server@11:dhcpv6-server@5:dns-dynamic@4:dns-forwarding@4:firewall@17:flow-accounting@1:https@6:ids@1:interfaces@33:ipoe-server@3:ipsec@13:isis@3:l2tp@9:lldp@2:mdns@1:monitoring@1:nat@8:nat66@3:ntp@3:openconnect@3:openvpn@4:ospf@2:pim@1:policy@8:pppoe-server@10:pptp@5:qos@2:quagga@11:reverse-proxy@1:rip@1:rpki@2:salt@1:snmp@3:ssh@2:sstp@6:system@27:vrf@3:vrrp@4:vyos-accel-ppp@2:wanloadbalance@3:webproxy@2"
// Release version: 1.5-rolling-202407300021

---

## Running configuration

interfaces {
bridge br0 {
member {
interface eth1 {
}
interface vxlan0 {
}
}
}
bridge br100 {
member {
interface eth1.100 {
}
interface vxlan100 {
}
}
}
bridge br200 {
member {
interface eth1.200 {
}
interface vxlan200 {
}
}
}
ethernet eth1 {
vif 100 {
}
vif 200 {
}
}
ethernet eth2 {
address 192.168.12.1/24
}
loopback lo {
address 10.1.1.1/32
}
vxlan vxlan0 {
source-address 10.1.1.1
vni 10000
}
vxlan vxlan100 {
source-address 10.1.1.1
vni 10100
}
vxlan vxlan200 {
source-address 10.1.1.1
vni 10200
}
}
protocols {
bgp {
address-family {
l2vpn-evpn {
advertise-all-vni
}
}
neighbor 10.2.2.2 {
address-family {
l2vpn-evpn {
}
}
ebgp-multihop 255
remote-as 65002
update-source 10.1.1.1
}
system-as 65001
timers {
holdtime 30
keepalive 10
}
}
ospf {
area 0 {
network 192.168.12.0/24
network 10.1.1.1/32
}
}
}
service {
ntp {
allow-client {
address 127.0.0.0/8
address 169.254.0.0/16
address 10.0.0.0/8
address 172.16.0.0/12
address 192.168.0.0/16
address ::1/128
address fe80::/10
address fc00::/7
}
server time1.vyos.net {
}
server time2.vyos.net {
}
server time3.vyos.net {
}
}
ssh {
}
}
system {
config-management {
commit-revisions 100
}
console {
device ttyS0 {
speed 115200
}
}
host-name vyos01
login {
user vyos {
authentication {
encrypted-password **\*\***\*\*\*\***\*\***
plaintext-password **\*\***\*\*\*\***\*\***
}
}
}
syslog {
global {
facility all {
level info
}
facility local7 {
level debug
}
}
}
}

---

## Package Repository Configuration File

---

## Repositories

total 0

---

## User Startup Scripts (Preconfig)

#!/bin/sh

# This script is executed at boot time before VyOS configuration is applied.

# Any modifications required to work around unfixed bugs or use

# services not available through the VyOS CLI system can be placed here.

---

## User Startup Scripts (Postconfig)

#!/bin/vbash

# This script is executed at boot time after VyOS configuration is fully applied.

# Any modifications required to work around unfixed bugs

# or use services not available through the VyOS CLI system can be placed here.

source /opt/vyatta/etc/functions/script-template

hostname=$(hostname)
configure
set system host-name $hostname
set service ssh
commit
exit

chown -R vyos:vyattacfg /config
chown -R vyos:vyattacfg /opt/vyatta/config
chown -R vyos:vyattacfg /opt/vyatta/etc/config

---

## FRR configuration

Building configuration...

Current configuration:
!
frr version 9.1.1
frr defaults traditional
hostname vyos01
log syslog
log facility local7
service integrated-vtysh-config
!
router bgp 65001
no bgp ebgp-requires-policy
no bgp default ipv4-unicast
no bgp network import-check
timers bgp 10 30
neighbor 10.2.2.2 remote-as 65002
neighbor 10.2.2.2 ebgp-multihop
neighbor 10.2.2.2 update-source 10.1.1.1
!
address-family l2vpn evpn
neighbor 10.2.2.2 activate
advertise-all-vni
exit-address-family
exit
!
router ospf
auto-cost reference-bandwidth 100
timers throttle spf 200 1000 10000
network 10.1.1.1/32 area 0
network 192.168.12.0/24 area 0
exit
!
rpki
exit
!
end

---

## Interfaces

Codes: S - State, L - Link, u - Up, D - Down, A - Admin Down
Interface IP Address MAC VRF MTU S/L Description

---

br0 - c2:83:76:25:28:7f default 1500 u/u
br100 - fa:a7:39:5d:62:82 default 1500 u/u
br200 - 26:0a:3c:8e:cd:f7 default 1500 u/u
eth0 172.20.20.4/24 02:42:ac:14:14:04 default 1500 u/u
2001:172:20:20::4/64
eth1 - aa:c1:ab:43:10:3a default 1500 u/u
eth1.100 - aa:c1:ab:43:10:3a default 1500 u/u
eth1.200 - aa:c1:ab:43:10:3a default 1500 u/u
eth2 192.168.12.1/24 aa:c1:ab:8a:e6:fe default 1500 u/u
lo 127.0.0.1/8 00:00:00:00:00:00 default 65536 u/u
10.1.1.1/32
::1/128
vxlan0 - 6e:b4:80:21:07:26 default 1500 u/u
vxlan100 - 76:86:fd:a7:2f:e0 default 1500 u/u
vxlan200 - 0a:91:21:4d:c6:a7 default 1500 u/u

---

## Interface statistics

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
RX: bytes packets errors dropped missed mcast
27312 382 0 0 0 0
TX: bytes packets errors dropped carrier collsns
27312 382 0 0 0 0
2: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/ipip 0.0.0.0 brd 0.0.0.0
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
3: ip6tnl0@NONE: <NOARP> mtu 1452 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/tunnel6 :: brd :: permaddr 66a4:8897:e8e3::
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
4: gre0@NONE: <NOARP> mtu 1476 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/gre 0.0.0.0 brd 0.0.0.0
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
5: gretap0@NONE: <BROADCAST,MULTICAST> mtu 1462 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
6: erspan0@NONE: <BROADCAST,MULTICAST> mtu 1450 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
7: pim6reg@NONE: <NOARP,UP,LOWER_UP> mtu 1452 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
link/pimreg
RX: bytes packets errors dropped missed mcast
0 0 0 0 0 0
TX: bytes packets errors dropped carrier collsns
0 0 0 0 0 0
8: br100: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
link/ether fa:a7:39:5d:62:82 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
1676 27 0 0 0 26
TX: bytes packets errors dropped carrier collsns
746 7 0 0 0 0
9: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
link/ether c2:83:76:25:28:7f brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
140 3 0 0 0 2
TX: bytes packets errors dropped carrier collsns
746 7 0 0 0 0
10: br200: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
link/ether 26:0a:3c:8e:cd:f7 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
1676 27 0 0 0 26
TX: bytes packets errors dropped carrier collsns
746 7 0 0 0 0
11: eth1.100@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br100 state UP mode DEFAULT group default qlen 1000
link/ether aa:c1:ab:43:10:3a brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
1632 25 0 1 0 13
TX: bytes packets errors dropped carrier collsns
3500 44 0 0 0 0
12: eth1.200@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br200 state UP mode DEFAULT group default qlen 1000
link/ether aa:c1:ab:43:10:3a brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
1048 17 0 2 0 13
TX: bytes packets errors dropped carrier collsns
2212 26 0 0 0 0
13: vxlan100: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br100 state UNKNOWN mode DEFAULT group default qlen 1000
link/ether 76:86:fd:a7:2f:e0 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
2064 35 0 1 0 0
TX: bytes packets errors dropped carrier collsns
1632 25 0 2 0 0
14: vxlan200: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br200 state UNKNOWN mode DEFAULT group default qlen 1000
link/ether 0a:91:21:4d:c6:a7 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
1048 17 0 1 0 0
TX: bytes packets errors dropped carrier collsns
1048 17 0 2 0 0
15: vxlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br0 state UNKNOWN mode DEFAULT group default qlen 1000
link/ether 6e:b4:80:21:07:26 brd ff:ff:ff:ff:ff:ff
RX: bytes packets errors dropped missed mcast
280 5 0 1 0 0
TX: bytes packets errors dropped carrier collsns
280 5 0 2 0 0
157: eth0@if158: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default
link/ether 02:42:ac:14:14:04 brd ff:ff:ff:ff:ff:ff link-netnsid 0
RX: bytes packets errors dropped missed mcast
216216 2072 0 0 0 0
TX: bytes packets errors dropped carrier collsns
426208 1609 0 0 0 0
162: eth1@if161: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br0 state UP mode DEFAULT group default
link/ether aa:c1:ab:43:10:3a brd ff:ff:ff:ff:ff:ff link-netnsid 2
RX: bytes packets errors dropped missed mcast
4764 62 0 0 0 0
TX: bytes packets errors dropped carrier collsns
7378 87 0 0 0 0
164: eth2@if163: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default
link/ether aa:c1:ab:8a:e6:fe brd ff:ff:ff:ff:ff:ff link-netnsid 1
RX: bytes packets errors dropped missed mcast
75489 894 0 0 0 0
TX: bytes packets errors dropped carrier collsns
67522 779 0 0 0 0

---

## Physical Interface statistics

---

## ethtool --driver eth0

driver: veth
version: 1.0
firmware-version:
expansion-rom-version:
bus-info:
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no

---

## ethtool --statistics eth0

NIC statistics:
peer_ifindex: 158
rx_queue_0_xdp_packets: 0
rx_queue_0_xdp_bytes: 0
rx_queue_0_drops: 0
rx_queue_0_xdp_redirect: 0
rx_queue_0_xdp_drops: 0
rx_queue_0_xdp_tx: 0
rx_queue_0_xdp_tx_errors: 0
tx_queue_0_xdp_xmit: 0
tx_queue_0_xdp_xmit_errors: 0

---

## ethtool --show-ring eth0

netlink error: Operation not supported

---

## ethtool --show-coalesce eth0

netlink error: Operation not supported

---

## ethtool --pause eth0

netlink error: Operation not permitted

---

## ethtool --show-features eth0

Features for eth0:
rx-checksumming: on
tx-checksumming: off
tx-checksum-ipv4: off [fixed]
tx-checksum-ip-generic: off
tx-checksum-ipv6: off [fixed]
tx-checksum-fcoe-crc: off [fixed]
tx-checksum-sctp: off
scatter-gather: on
tx-scatter-gather: on
tx-scatter-gather-fraglist: on
tcp-segmentation-offload: off
tx-tcp-segmentation: off [requested on]
tx-tcp-ecn-segmentation: off [requested on]
tx-tcp-mangleid-segmentation: off [requested on]
tx-tcp6-segmentation: off [requested on]
generic-segmentation-offload: on
generic-receive-offload: off
large-receive-offload: off [fixed]
rx-vlan-offload: on
tx-vlan-offload: on
ntuple-filters: off [fixed]
receive-hashing: off [fixed]
highdma: on
rx-vlan-filter: off [fixed]
vlan-challenged: off [fixed]
tx-lockless: on [fixed]
netns-local: off [fixed]
tx-gso-robust: off [fixed]
tx-fcoe-segmentation: off [fixed]
tx-gre-segmentation: on
tx-gre-csum-segmentation: on
tx-ipxip4-segmentation: on
tx-ipxip6-segmentation: on
tx-udp_tnl-segmentation: on
tx-udp_tnl-csum-segmentation: on
tx-gso-partial: off [fixed]
tx-tunnel-remcsum-segmentation: off [fixed]
tx-sctp-segmentation: on
tx-esp-segmentation: off [fixed]
tx-udp-segmentation: on
tx-gso-list: on
fcoe-mtu: off [fixed]
tx-nocache-copy: off
loopback: off [fixed]
rx-fcs: off [fixed]
rx-all: off [fixed]
tx-vlan-stag-hw-insert: on
rx-vlan-stag-hw-parse: on
rx-vlan-stag-filter: off [fixed]
l2-fwd-offload: off [fixed]
hw-tc-offload: off [fixed]
esp-hw-offload: off [fixed]
esp-tx-csum-hw-offload: off [fixed]
rx-udp_tunnel-port-offload: off [fixed]
tls-hw-tx-offload: off [fixed]
tls-hw-rx-offload: off [fixed]
rx-gro-hw: off [fixed]
tls-hw-record: off [fixed]
rx-gro-list: off
macsec-hw-offload: off [fixed]
rx-udp-gro-forwarding: off
hsr-tag-ins-offload: off [fixed]
hsr-tag-rm-offload: off [fixed]
hsr-fwd-offload: off [fixed]
hsr-dup-offload: off [fixed]

---

## ethtool --phy-statistics eth0

no stats available

---

## ethtool --driver eth1

driver: veth
version: 1.0
firmware-version:
expansion-rom-version:
bus-info:
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no

---

## ethtool --statistics eth1

NIC statistics:
peer_ifindex: 161
rx_queue_0_xdp_packets: 0
rx_queue_0_xdp_bytes: 0
rx_queue_0_drops: 0
rx_queue_0_xdp_redirect: 0
rx_queue_0_xdp_drops: 0
rx_queue_0_xdp_tx: 0
rx_queue_0_xdp_tx_errors: 0
tx_queue_0_xdp_xmit: 0
tx_queue_0_xdp_xmit_errors: 0

---

## ethtool --show-ring eth1

netlink error: Operation not supported

---

## ethtool --show-coalesce eth1

netlink error: Operation not supported

---

## ethtool --pause eth1

netlink error: Operation not permitted

---

## ethtool --show-features eth1

Features for eth1:
rx-checksumming: on
tx-checksumming: off
tx-checksum-ipv4: off [fixed]
tx-checksum-ip-generic: off
tx-checksum-ipv6: off [fixed]
tx-checksum-fcoe-crc: off [fixed]
tx-checksum-sctp: off
scatter-gather: off
tx-scatter-gather: off
tx-scatter-gather-fraglist: off
tcp-segmentation-offload: off
tx-tcp-segmentation: off [requested on]
tx-tcp-ecn-segmentation: off [requested on]
tx-tcp-mangleid-segmentation: off [requested on]
tx-tcp6-segmentation: off [requested on]
generic-segmentation-offload: off
generic-receive-offload: off
large-receive-offload: off [fixed]
rx-vlan-offload: on
tx-vlan-offload: on
ntuple-filters: off [fixed]
receive-hashing: off [fixed]
highdma: on
rx-vlan-filter: off [fixed]
vlan-challenged: off [fixed]
tx-lockless: on [fixed]
netns-local: off [fixed]
tx-gso-robust: off [fixed]
tx-fcoe-segmentation: off [fixed]
tx-gre-segmentation: on
tx-gre-csum-segmentation: on
tx-ipxip4-segmentation: on
tx-ipxip6-segmentation: on
tx-udp_tnl-segmentation: on
tx-udp_tnl-csum-segmentation: on
tx-gso-partial: off [fixed]
tx-tunnel-remcsum-segmentation: off [fixed]
tx-sctp-segmentation: on
tx-esp-segmentation: off [fixed]
tx-udp-segmentation: on
tx-gso-list: on
fcoe-mtu: off [fixed]
tx-nocache-copy: off
loopback: off [fixed]
rx-fcs: off [fixed]
rx-all: off [fixed]
tx-vlan-stag-hw-insert: on
rx-vlan-stag-hw-parse: on
rx-vlan-stag-filter: off [fixed]
l2-fwd-offload: off [fixed]
hw-tc-offload: off [fixed]
esp-hw-offload: off [fixed]
esp-tx-csum-hw-offload: off [fixed]
rx-udp_tunnel-port-offload: off [fixed]
tls-hw-tx-offload: off [fixed]
tls-hw-rx-offload: off [fixed]
rx-gro-hw: off [fixed]
tls-hw-record: off [fixed]
rx-gro-list: off
macsec-hw-offload: off [fixed]
rx-udp-gro-forwarding: off
hsr-tag-ins-offload: off [fixed]
hsr-tag-rm-offload: off [fixed]
hsr-fwd-offload: off [fixed]
hsr-dup-offload: off [fixed]

---

## ethtool --phy-statistics eth1

no stats available

---

## ethtool --driver eth2

driver: veth
version: 1.0
firmware-version:
expansion-rom-version:
bus-info:
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no

---

## ethtool --statistics eth2

NIC statistics:
peer_ifindex: 163
rx_queue_0_xdp_packets: 0
rx_queue_0_xdp_bytes: 0
rx_queue_0_drops: 0
rx_queue_0_xdp_redirect: 0
rx_queue_0_xdp_drops: 0
rx_queue_0_xdp_tx: 0
rx_queue_0_xdp_tx_errors: 0
tx_queue_0_xdp_xmit: 0
tx_queue_0_xdp_xmit_errors: 0

---

## ethtool --show-ring eth2

netlink error: Operation not supported

---

## ethtool --show-coalesce eth2

netlink error: Operation not supported

---

## ethtool --pause eth2

netlink error: Operation not permitted

---

## ethtool --show-features eth2

Features for eth2:
rx-checksumming: on
tx-checksumming: off
tx-checksum-ipv4: off [fixed]
tx-checksum-ip-generic: off
tx-checksum-ipv6: off [fixed]
tx-checksum-fcoe-crc: off [fixed]
tx-checksum-sctp: off
scatter-gather: off
tx-scatter-gather: off
tx-scatter-gather-fraglist: off
tcp-segmentation-offload: off
tx-tcp-segmentation: off [requested on]
tx-tcp-ecn-segmentation: off [requested on]
tx-tcp-mangleid-segmentation: off [requested on]
tx-tcp6-segmentation: off [requested on]
generic-segmentation-offload: off
generic-receive-offload: off
large-receive-offload: off [fixed]
rx-vlan-offload: on
tx-vlan-offload: on
ntuple-filters: off [fixed]
receive-hashing: off [fixed]
highdma: on
rx-vlan-filter: off [fixed]
vlan-challenged: off [fixed]
tx-lockless: on [fixed]
netns-local: off [fixed]
tx-gso-robust: off [fixed]
tx-fcoe-segmentation: off [fixed]
tx-gre-segmentation: on
tx-gre-csum-segmentation: on
tx-ipxip4-segmentation: on
tx-ipxip6-segmentation: on
tx-udp_tnl-segmentation: on
tx-udp_tnl-csum-segmentation: on
tx-gso-partial: off [fixed]
tx-tunnel-remcsum-segmentation: off [fixed]
tx-sctp-segmentation: on
tx-esp-segmentation: off [fixed]
tx-udp-segmentation: on
tx-gso-list: on
fcoe-mtu: off [fixed]
tx-nocache-copy: off
loopback: off [fixed]
rx-fcs: off [fixed]
rx-all: off [fixed]
tx-vlan-stag-hw-insert: on
rx-vlan-stag-hw-parse: on
rx-vlan-stag-filter: off [fixed]
l2-fwd-offload: off [fixed]
hw-tc-offload: off [fixed]
esp-hw-offload: off [fixed]
esp-tx-csum-hw-offload: off [fixed]
rx-udp_tunnel-port-offload: off [fixed]
tls-hw-tx-offload: off [fixed]
tls-hw-rx-offload: off [fixed]
rx-gro-hw: off [fixed]
tls-hw-record: off [fixed]
rx-gro-list: off
macsec-hw-offload: off [fixed]
rx-udp-gro-forwarding: off
hsr-tag-ins-offload: off [fixed]
hsr-tag-rm-offload: off [fixed]
hsr-fwd-offload: off [fixed]
hsr-dup-offload: off [fixed]

---

## ethtool --phy-statistics eth2

no stats available

---

## netstat --interfaces

Kernel Interface table
Iface MTU RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
br0 1500 3 0 0 0 7 0 0 0 BMRU
br100 1500 27 0 0 0 7 0 0 0 BMRU
br200 1500 27 0 0 0 7 0 0 0 BMRU
eth0 1500 2122 0 0 0 1660 0 0 0 BMRU
eth1 1500 62 0 0 0 87 0 0 0 BMRU
eth2 1500 894 0 0 0 779 0 0 0 BMRU
eth1.100 1500 25 0 1 0 44 0 0 0 BMRU
eth1.200 1500 17 0 2 0 26 0 0 0 BMRU
lo 65536 382 0 0 0 382 0 0 0 LRU
pim6reg 1452 0 0 0 0 0 0 0 0 ORU
vxlan0 1500 5 0 1 0 5 0 2 0 BMRU
vxlan100 1500 35 0 1 0 25 0 2 0 BMRU
vxlan200 1500 17 0 1 0 17 0 2 0 BMRU

---

## netstat --listening

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 localhost:2623 0.0.0.0:_ LISTEN
tcp 0 0 localhost:2616 0.0.0.0:_ LISTEN
tcp 0 0 localhost:2617 0.0.0.0:_ LISTEN
tcp 0 0 localhost:2612 0.0.0.0:_ LISTEN
tcp 0 0 localhost:isisd 0.0.0.0:_ LISTEN
tcp 0 0 localhost:2609 0.0.0.0:_ LISTEN
tcp 0 0 localhost:ospfd 0.0.0.0:_ LISTEN
tcp 0 0 localhost:bgpd 0.0.0.0:_ LISTEN
tcp 0 0 localhost:ripd 0.0.0.0:_ LISTEN
tcp 0 0 localhost:zebra 0.0.0.0:_ LISTEN
tcp 0 0 127.0.0.11:36427 0.0.0.0:_ LISTEN
tcp 0 0 0.0.0.0:ssh 0.0.0.0:_ LISTEN
tcp 0 0 0.0.0.0:bgp 0.0.0.0:_ LISTEN
tcp6 0 0 localhost:ripngd [::]:_ LISTEN
tcp6 0 0 localhost:ospf6d [::]:_ LISTEN
tcp6 0 0 localhost:2622 [::]:_ LISTEN
tcp6 0 0 [::]:ssh [::]:_ LISTEN
tcp6 0 0 [::]:bgp [::]:_ LISTEN
udp 0 0 127.0.0.11:34436 0.0.0.0:_
udp 0 0 0.0.0.0:3784 0.0.0.0:_
udp 0 0 0.0.0.0:ntp 0.0.0.0:_
udp 0 0 localhost:323 0.0.0.0:_
udp 0 0 0.0.0.0:4784 0.0.0.0:_
udp 0 0 0.0.0.0:4789 0.0.0.0:_
udp6 0 0 [::]:3784 [::]:_
udp6 0 0 [::]:3785 [::]:_
udp6 0 0 [::]:ntp [::]:_
udp6 0 0 localhost:323 [::]:_
udp6 0 0 [::]:4784 [::]:_
raw 0 0 0.0.0.0:ospf 0.0.0.0:_ 7
raw 2304 0 0.0.0.0:ospf 0.0.0.0:_ 7
raw 0 0 0.0.0.0:ospf 0.0.0.0:_ 7
raw 0 0 0.0.0.0:255 0.0.0.0:_ 7
raw6 0 0 [::]:ipv6-icmp [::]:_ 7
raw6 47360 0 [::]:ipv6-icmp [::]:_ 7
raw6 0 0 [::]:pim [::]:_ 7
Active UNIX domain sockets (only servers)
Proto RefCnt Flags Type State I-Node Path
unix 2 [ ACC ] STREAM LISTENING 26870233 /run/vyos-configd.sock
unix 2 [ ACC ] STREAM LISTENING 26894735 /run/user/1002/systemd/private
unix 2 [ ACC ] STREAM LISTENING 26856945 /run/systemd/private
unix 2 [ ACC ] STREAM LISTENING 26856947 /run/systemd/userdb/io.systemd.DynamicUser
unix 2 [ ACC ] STREAM LISTENING 26856948 /run/systemd/io.system.ManagedOOM
unix 2 [ ACC ] STREAM LISTENING 26857919 /run/systemd/journal/stdout
unix 2 [ ACC ] SEQPACKET LISTENING 26857921 /run/udev/control
unix 2 [ ACC ] STREAM LISTENING 26857988 /run/systemd/journal/io.systemd.journal
unix 2 [ ACC ] STREAM LISTENING 26862559 /run/vyos-hostsd/vyos-hostsd.sock
unix 2 [ ACC ] STREAM LISTENING 26877159 /var/run/frr/watchfrr.vty
unix 2 [ ACC ] STREAM LISTENING 26877218 /var/run/frr/zserv.api
unix 2 [ ACC ] STREAM LISTENING 26877220 /var/run/frr/zebra.vty
unix 2 [ ACC ] STREAM LISTENING 26875779 /var/run/frr/mgmtd_fe.sock
unix 2 [ ACC ] STREAM LISTENING 26875780 /var/run/frr/mgmtd_be.sock
unix 2 [ ACC ] STREAM LISTENING 26876184 /var/run/frr/mgmtd.vty
unix 2 [ ACC ] STREAM LISTENING 26876205 /var/run/frr/bgpd.vty
unix 2 [ ACC ] STREAM LISTENING 26875830 /var/run/frr/ripd.vty
unix 2 [ ACC ] STREAM LISTENING 26878109 /var/run/frr/ripngd.vty
unix 2 [ ACC ] STREAM LISTENING 26878986 /var/run/frr/ospfd.vty
unix 2 [ ACC ] STREAM LISTENING 26876268 /var/run/frr/ospf6d.vty
unix 2 [ ACC ] STREAM LISTENING 26878175 /var/run/frr/isisd.vty
unix 2 [ ACC ] STREAM LISTENING 26876300 /var/run/frr/babeld.vty
unix 2 [ ACC ] STREAM LISTENING 26864352 /run/dbus/system_bus_socket
unix 2 [ ACC ] STREAM LISTENING 26877495 /var/run/frr/pim6d.vty
unix 2 [ ACC ] STREAM LISTENING 26864354 /run/uuidd/request
unix 2 [ ACC ] STREAM LISTENING 26876331 /var/run/frr/ldpd.vty
unix 2 [ ACC ] STREAM LISTENING 26879180 /var/run/frr/ldpd.sock
unix 2 [ ACC ] STREAM LISTENING 26879199 /var/run/frr/staticd.vty
unix 2 [ ACC ] STREAM LISTENING 26879212 /var/run/frr/bfdd.sock
unix 2 [ ACC ] STREAM LISTENING 26876372 /var/run/frr/bfdd.vty

---

## cat /proc/net/dev

Inter-| Receive | Transmit
face |bytes packets errs drop fifo frame compressed multicast|bytes packets errs drop fifo colls carrier compressed
lo: 27644 386 0 0 0 0 0 0 27644 386 0 0 0 0 0 0
tunl0: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
ip6tnl0: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
gre0: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
gretap0: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
erspan0: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
pim6reg: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
br100: 1676 27 0 0 0 0 0 26 746 7 0 0 0 0 0 0
br0: 140 3 0 0 0 0 0 2 746 7 0 0 0 0 0 0
br200: 1676 27 0 0 0 0 0 26 746 7 0 0 0 0 0 0
eth1.100: 1632 25 0 1 0 0 0 13 3500 44 0 0 0 0 0 0
eth1.200: 1048 17 0 2 0 0 0 13 2212 26 0 0 0 0 0 0
vxlan100: 2064 35 0 1 0 0 0 0 1632 25 0 2 0 0 0 0
vxlan200: 1048 17 0 1 0 0 0 0 1048 17 0 2 0 0 0 0
vxlan0: 280 5 0 1 0 0 0 0 280 5 0 2 0 0 0 0
eth0: 221548 2134 0 0 0 0 0 0 460254 1672 0 0 0 0 0 0
eth1: 4764 62 0 0 0 0 0 0 7378 87 0 0 0 0 0 0
eth2: 75489 894 0 0 0 0 0 0 67522 779 0 0 0 0 0 0

---

## Show bridge

Bridge interface br200:
Member State MTU Flags Prio

---

eth1.200 forwarding 1500 broadcast,multicast,up,lower_up 32
vxlan200 forwarding 1500 broadcast,multicast,up,lower_up 32

Bridge interface br100:
Member State MTU Flags Prio

---

eth1.100 forwarding 1500 broadcast,multicast,up,lower_up 32
vxlan100 forwarding 1500 broadcast,multicast,up,lower_up 32

Bridge interface br0:
Member State MTU Flags Prio

---

eth1 forwarding 1500 broadcast,multicast,up,lower_up 32
vxlan0 forwarding 1500 broadcast,multicast,up,lower_up 32

---

## ARP Table (Total entries)

Address Interface Link layer address State

---

192.168.12.2 eth2 aa:c1:ab:38:f7:ef REACHABLE

---

## show ipv6 neighbors

Address Interface Link layer address State

---

fe80::42:acff:fe14:1406 eth0 02:42:ac:14:14:06 STALE
2001:172:20:20::1 eth0 02:42:78:24:66:df REACHABLE
fe80::a8c1:abff:feba:87d6 br200 aa:c1:ab:ba:87:d6 STALE
fe80::a8c1:abff:feba:87d6 br100 aa:c1:ab:ba:87:d6 STALE

---

## show ip route bgp | head -108

---

## show ip route cache

---

## show ip route connected

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

C>_ 10.1.1.1/32 is directly connected, lo, 00:58:34
C>_ 172.20.20.0/24 is directly connected, eth0, 01:25:39
C>\* 192.168.12.0/24 is directly connected, eth2, 00:58:33

---

## show ip route forward

default via 172.20.20.1 dev eth0
10.2.2.2 nhid 24 via 192.168.12.2 dev eth2 proto ospf metric 20
10.3.3.3 nhid 24 via 192.168.12.2 dev eth2 proto ospf metric 20
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.4
192.168.12.0/24 dev eth2 proto kernel scope link src 192.168.12.1
192.168.23.0/24 nhid 24 via 192.168.12.2 dev eth2 proto ospf metric 20

---

## show ip route isis | head -108

---

## show ip route kernel

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

K>\* 0.0.0.0/0 [0/0] via 172.20.20.1, eth0, 01:25:41

---

## show ip route ospf | head -108

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

O 10.1.1.1/32 [110/0] is directly connected, lo, weight 1, 00:58:31
O>_ 10.2.2.2/32 [110/1] via 192.168.12.2, eth2, weight 1, 00:55:58
O>_ 10.3.3.3/32 [110/2] via 192.168.12.2, eth2, weight 1, 00:52:52
O 192.168.12.0/24 [110/1] is directly connected, eth2, weight 1, 00:58:31
O>\* 192.168.23.0/24 [110/2] via 192.168.12.2, eth2, weight 1, 00:55:58

---

## show ip route rip

---

## show ip route static

---

## show ip route summary

Route Source Routes FIB (vrf default)
kernel 1 1
connected 3 3
ospf 5 3

---

Totals 9 7

---

## show ip route supernets-only

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

K>\* 0.0.0.0/0 [0/0] via 172.20.20.1, eth0, 01:25:45

---

## show ip route table all

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

VRF default table 254:
K>_ 0.0.0.0/0 [0/0] via 172.20.20.1, eth0, 01:25:46
O 10.1.1.1/32 [110/0] is directly connected, lo, weight 1, 00:58:36
C>_ 10.1.1.1/32 is directly connected, lo, 00:58:41
O>_ 10.2.2.2/32 [110/1] via 192.168.12.2, eth2, weight 1, 00:56:03
O>_ 10.3.3.3/32 [110/2] via 192.168.12.2, eth2, weight 1, 00:52:57
C>_ 172.20.20.0/24 is directly connected, eth0, 01:25:46
O 192.168.12.0/24 [110/1] is directly connected, eth2, weight 1, 00:58:36
C>_ 192.168.12.0/24 is directly connected, eth2, 00:58:40
O>\* 192.168.23.0/24 [110/2] via 192.168.12.2, eth2, weight 1, 00:56:03

---

## show ip route vrf all

Codes: K - kernel route, C - connected, S - static, R - RIP,
O - OSPF, I - IS-IS, B - BGP, E - EIGRP, N - NHRP,
T - Table, v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

VRF default:
K>_ 0.0.0.0/0 [0/0] via 172.20.20.1, eth0, 01:25:47
O 10.1.1.1/32 [110/0] is directly connected, lo, weight 1, 00:58:37
C>_ 10.1.1.1/32 is directly connected, lo, 00:58:42
O>_ 10.2.2.2/32 [110/1] via 192.168.12.2, eth2, weight 1, 00:56:04
O>_ 10.3.3.3/32 [110/2] via 192.168.12.2, eth2, weight 1, 00:52:58
C>_ 172.20.20.0/24 is directly connected, eth0, 01:25:47
O 192.168.12.0/24 [110/1] is directly connected, eth2, weight 1, 00:58:37
C>_ 192.168.12.0/24 is directly connected, eth2, 00:58:41
O>\* 192.168.23.0/24 [110/2] via 192.168.12.2, eth2, weight 1, 00:56:04

---

## show ipv6 route bgp | head -108

---

## show ipv6 route cache

---

## show ipv6 route connected

Codes: K - kernel route, C - connected, S - static, R - RIPng,
O - OSPFv3, I - IS-IS, B - BGP, N - NHRP, T - Table,
v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

C>_ 2001:172:20:20::/64 is directly connected, eth0, 01:25:49
C _ fe80::/64 is directly connected, br200, 00:48:07
C _ fe80::/64 is directly connected, br100, 00:48:07
C _ fe80::/64 is directly connected, br0, 00:48:08
C>_ fe80::/64 is directly connected, lo, 01:25:31
C _ fe80::/64 is directly connected, eth2, 01:25:49
C \* fe80::/64 is directly connected, eth0, 01:25:49

---

## show ipv6 route forward

2001:172:20:20::/64 dev eth0 proto kernel metric 256 pref medium
fe80::/64 dev eth0 proto kernel metric 256 pref medium
fe80::/64 dev eth2 proto kernel metric 256 pref medium
fe80::/64 dev lo proto kernel metric 256 pref medium
fe80::/64 dev br100 proto kernel metric 256 pref medium
fe80::/64 dev br0 proto kernel metric 256 pref medium
fe80::/64 dev br200 proto kernel metric 256 pref medium
default via 2001:172:20:20::1 dev eth0 metric 1024 pref medium

---

## show ipv6 route isis

---

## show ipv6 route kernel

Codes: K - kernel route, C - connected, S - static, R - RIPng,
O - OSPFv3, I - IS-IS, B - BGP, N - NHRP, T - Table,
v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

K>\* ::/0 [0/1024] via 2001:172:20:20::1, eth0, 01:25:51

---

## show ipv6 route ospfv3

---

## show ipv6 route rip

---

## show ipv6 route static

---

## show ipv6 route summary

Route Source Routes FIB (vrf default)
kernel 1 1
connected 7 7

---

Totals 8 8

---

## show ipv6 route table all

Codes: K - kernel route, C - connected, S - static, R - RIPng,
O - OSPFv3, I - IS-IS, B - BGP, N - NHRP, T - Table,
v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

VRF default table 254:
K>_ ::/0 [0/1024] via 2001:172:20:20::1, eth0, 01:25:55
C>_ 2001:172:20:20::/64 is directly connected, eth0, 01:25:55
C _ fe80::/64 is directly connected, br200, 00:48:13
C _ fe80::/64 is directly connected, br100, 00:48:13
C _ fe80::/64 is directly connected, br0, 00:48:14
C>_ fe80::/64 is directly connected, lo, 01:25:37
C _ fe80::/64 is directly connected, eth2, 01:25:55
C _ fe80::/64 is directly connected, eth0, 01:25:55

---

## show ipv6 route vrf all

Codes: K - kernel route, C - connected, S - static, R - RIPng,
O - OSPFv3, I - IS-IS, B - BGP, N - NHRP, T - Table,
v - VNC, V - VNC-Direct, A - Babel, F - PBR,
f - OpenFabric, > - selected route, \* - FIB route, q - queued, r - rejected, b - backup
t - trapped, o - offload failure

VRF default:
K>_ ::/0 [0/1024] via 2001:172:20:20::1, eth0, 01:25:56
C>_ 2001:172:20:20::/64 is directly connected, eth0, 01:25:56
C _ fe80::/64 is directly connected, br200, 00:48:14
C _ fe80::/64 is directly connected, br100, 00:48:14
C _ fe80::/64 is directly connected, br0, 00:48:15
C>_ fe80::/64 is directly connected, lo, 01:25:38
C _ fe80::/64 is directly connected, eth2, 01:25:56
C _ fe80::/64 is directly connected, eth0, 01:25:56

---

## nft list ruleset

# Warning: table ip nat is managed by iptables-nft, do not touch!

table ip nat {
chain DOCKER_OUTPUT {
meta l4proto tcp ip daddr 127.0.0.11 tcp dport 53 counter packets 0 bytes 0 dnat to 127.0.0.11:36427
meta l4proto udp ip daddr 127.0.0.11 udp dport 53 counter packets 0 bytes 0 dnat to 127.0.0.11:34436
}

        chain OUTPUT {
                type nat hook output priority dstnat; policy accept;
                ip daddr 127.0.0.11 counter packets 0 bytes 0 jump DOCKER_OUTPUT
        }

        chain DOCKER_POSTROUTING {
                meta l4proto tcp ip saddr 127.0.0.11 tcp sport 36427 counter packets 0 bytes 0 snat to :53
                meta l4proto udp ip saddr 127.0.0.11 udp sport 34436 counter packets 0 bytes 0 snat to :53
        }

        chain POSTROUTING {
                type nat hook postrouting priority srcnat; policy accept;
                ip daddr 127.0.0.11 counter packets 0 bytes 0 jump DOCKER_POSTROUTING
        }

        chain VYOS_PRE_SNAT_HOOK {
                type nat hook postrouting priority srcnat - 1; policy accept;
                return
        }

}
table inet mangle {
chain FORWARD {
type filter hook forward priority mangle; policy accept;
}
}
table ip raw {
chain VYOS_TCP_MSS {
type filter hook forward priority raw; policy accept;
}

        chain vyos_global_rpfilter {
                return
        }

        chain vyos_rpfilter {
                type filter hook prerouting priority raw; policy accept;
                counter packets 1306 bytes 92658 jump vyos_global_rpfilter
        }

        chain VYOS_PREROUTING_HOOK {
                type filter hook prerouting priority raw; policy accept;
        }

}
table ip6 raw {
chain VYOS_TCP_MSS {
type filter hook forward priority raw; policy accept;
}

        chain vyos_global_rpfilter {
                return
        }

        chain vyos_rpfilter {
                type filter hook prerouting priority raw; policy accept;
                counter packets 2202 bytes 195264 jump vyos_global_rpfilter
        }

        chain VYOS_PREROUTING_HOOK {
                type filter hook prerouting priority raw; policy accept;
        }

}
table inet vrf_zones {
map ct_iface_map {
typeof iifname : ct zone
}

        chain vrf_zones_ct_in {
                type filter hook prerouting priority raw; policy accept;
        }

        chain vrf_zones_ct_out {
                type filter hook output priority raw; policy accept;
        }

}
table ip vyos_conntrack {
chain VYOS_CT_IGNORE {
return
}

        chain VYOS_CT_TIMEOUT {
                return
        }

        chain PREROUTING {
                type filter hook prerouting priority raw; policy accept;
                counter packets 1306 bytes 92658 jump VYOS_CT_IGNORE
                counter packets 1306 bytes 92658 jump VYOS_CT_TIMEOUT
                counter packets 1306 bytes 92658 jump FW_CONNTRACK
                counter packets 1306 bytes 92658 jump NAT_CONNTRACK
                counter packets 1306 bytes 92658 jump WLB_CONNTRACK
                notrack
        }

        chain OUTPUT {
                type filter hook output priority raw; policy accept;
                counter packets 1159 bytes 83893 jump VYOS_CT_IGNORE
                counter packets 1159 bytes 83893 jump VYOS_CT_TIMEOUT
                counter packets 1159 bytes 83893 jump FW_CONNTRACK
                counter packets 1159 bytes 83893 jump NAT_CONNTRACK
                notrack
        }

        chain VYOS_CT_HELPER {
                return
        }

        chain FW_CONNTRACK {
                return
        }

        chain NAT_CONNTRACK {
                return
        }

        chain WLB_CONNTRACK {
                return
        }

}
table ip6 vyos_conntrack {
chain VYOS_CT_IGNORE {
return
}

        chain VYOS_CT_TIMEOUT {
                return
        }

        chain PREROUTING {
                type filter hook prerouting priority raw; policy accept;
                counter packets 2201 bytes 195208 jump VYOS_CT_IGNORE
                counter packets 2201 bytes 195208 jump VYOS_CT_TIMEOUT
                counter packets 2201 bytes 195208 jump FW_CONNTRACK
                counter packets 2201 bytes 195208 jump NAT_CONNTRACK
                notrack
        }

        chain OUTPUT {
                type filter hook output priority raw; policy accept;
                counter packets 1723 bytes 457258 jump VYOS_CT_IGNORE
                counter packets 1723 bytes 457258 jump VYOS_CT_TIMEOUT
                counter packets 1723 bytes 457258 jump FW_CONNTRACK
                counter packets 1723 bytes 457258 jump NAT_CONNTRACK
                notrack
        }

        chain VYOS_CT_HELPER {
                return
        }

        chain FW_CONNTRACK {
                return
        }

        chain NAT_CONNTRACK {
                return
        }

}

---

## Show System Version

Version: VyOS 1.5-rolling-202407300021
Release train: current
Release flavor: generic

Built by: autobuild@vyos.net
Built on: Tue 30 Jul 2024 02:54 UTC
Build UUID: 34639626-cff6-4000-b1a2-ea261788fd3b
Build commit ID: bf3c5d3ac25f11

Architecture: x86_64
Boot via: installed image
System type: QEMU guest

Hardware vendor: QEMU
Hardware model: Standard PC (Q35 + ICH9, 2009)
Hardware S/N:
Hardware UUID: Unknown

Copyright: VyOS maintainers and contributors

---

## Show System Storage

Storage statistics are not available

---

## Show System Image Details

Traceback (most recent call last):
File "/usr/libexec/vyos/op_mode/image_info.py", line 106, in <module>
res = opmode.run(sys.modules[__name__])
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "/usr/lib/python3/dist-packages/vyos/opmode.py", line 271, in run
res = func(\*\*args)
^^^^^^^^^^^^
File "/usr/libexec/vyos/op_mode/image_info.py", line 101, in show_images_details
return \_format_show_images_details(images_details)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "/usr/libexec/vyos/op_mode/image_info.py", line 70, in \_format_show_images_details
tabulated: str = tabulate(table_data, headers,
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "/usr/lib/python3/dist-packages/tabulate.py", line 1601, in tabulate
aligns[idx] = align

````^^^^^
IndexError: list assignment index out of range

---

## Current Time

Sun Sep 1 16:02:54 UTC 2024

---

## Installed Packages

Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
+++-====================================-=================================================-============-================================================================================
ii aardvark-dns 1.4.0-3 amd64 Container-focused DNS server
ii accel-ppp 1.13.0 amd64 PPtP/L2TP/PPPoE/SSTP server for Linux
ii acpid 1:2.0.33-2+b1 amd64 Advanced Configuration and Power Interface event daemon
ii adduser 3.134 all add and remove users and groups
ii apt 2.6.1 amd64 commandline package manager
ii apt-utils 2.6.1 amd64 package management related utility programs
ii aptitude 0.8.13-5 amd64 terminal-based package manager
ii aptitude-common 0.8.13-5 all architecture independent files for the aptitude package manager
ii arpwatch 2.1a15-8+b1 amd64 Ethernet/FDDI station activity monitor
ii at 3.2.5-1+b1 amd64 Delayed job execution and batch processing
ii atop 2.8.1-1 amd64 Monitor for system resources and process activity
ii auditd 1:3.0.9-1 amd64 User space tools for security auditing
ii avahi-daemon 0.8-10 amd64 Avahi mDNS/DNS-SD daemon
ii aws-gwlbtun 20230915094114-f78058a-1 amd64 auto-generated package by debmake
ii base-files 12.4+deb12u6 amd64 Debian base system miscellaneous files
ii base-passwd 3.6.1 amd64 Debian base system master password and group files
ii bash 5.2.15-2+b7 amd64 GNU Bourne Again SHell
ii bash-completion 1:2.8-6 all programmable completion for the bash shell
ii beep 1.4.9-1+b1 amd64 advanced PC-speaker beeper
ii bgpq3 0.1.36.1-1 amd64 automatic BGP filter generator using RADB data
ii bind9-dnsutils 1:9.18.28-1~deb12u2 amd64 Clients provided with BIND 9
ii bind9-host 1:9.18.28-1~deb12u2 amd64 DNS Lookup Utility
ii bind9-libs:amd64 1:9.18.28-1~deb12u2 amd64 Shared Libraries used by BIND 9
ii bmon 1:4.0-10 amd64 portable bandwidth monitor and rate estimator
ii bsdextrautils 2.38.1-5+deb12u1 amd64 extra utilities from 4.4BSD-Lite
ii bsdmainutils 12.1.8 all Transitional package for more utilities from FreeBSD
ii bsdutils 1:2.38.1-5+deb12u1 amd64 basic utilities from 4.4BSD-Lite
ii busybox 1:1.35.0-4+b3 amd64 Tiny utilities for small and embedded systems
ii ca-certificates 20230311 all Common CA certificates
ii certbot 2.1.0-4 all automatically configure HTTPS using Let's Encrypt
ii charon-systemd 5.9.11-2+vyos0 amd64 strongSwan IPsec client, systemd support
ii chrony 4.3-2+deb12u1 amd64 Versatile implementation of the Network Time Protocol
ii cme 1.038-1 all Check or edit configuration data with Config::Model
ii conmon 2.1.6+ds1-1 amd64 OCI container runtime monitor
ii conntrack 1:1.4.7-1+b2 amd64 Program to modify the conntrack tables
ii conntrackd 1:1.4.7-1+b2 amd64 Connection tracking daemon
ii conserver-client 8.2.7-2+b1 amd64 connect to a console server
ii conserver-server 8.2.7-2+b1 amd64 connect multiple user to a serial console with logging
ii console-data 2:1.12-9 all keymaps, fonts, charset maps, fallback tables for 'kbd'.
ii coreutils 9.1-1 amd64 GNU core utilities
ii cpio 2.13+dfsg-7.1 amd64 GNU cpio -- a program to manage archives of files
ii cron 3.0pl1-162 amd64 process scheduling daemon
ii cron-daemon-common 3.0pl1-162 all process scheduling daemon's configuration files
ii crun 1.8.1-1+deb12u1 amd64 lightweight OCI runtime for running containers
ii cryptsetup 2:2.6.1-4~deb12u2 amd64 disk encryption support - startup scripts
ii cryptsetup-bin 2:2.6.1-4~deb12u2 amd64 disk encryption support - command line tools
ii curl 7.88.1-10+deb12u6 amd64 command line tool for transferring data with URL syntax
ii dash 0.5.12-2 amd64 POSIX-compliant shell
ii dbus 1.14.10-1~deb12u1 amd64 simple interprocess messaging system (system message bus)
ii dbus-bin 1.14.10-1~deb12u1 amd64 simple interprocess messaging system (command line utilities)
ii dbus-daemon 1.14.10-1~deb12u1 amd64 simple interprocess messaging system (reference message bus)
ii dbus-session-bus-common 1.14.10-1~deb12u1 all simple interprocess messaging system (session bus configuration)
ii dbus-system-bus-common 1.14.10-1~deb12u1 all simple interprocess messaging system (system bus configuration)
ii dctrl-tools 2.24-3+b1 amd64 Command-line tools to process Debian package information
ii ddclient 3.11.2-1 all address updating utility for dynamic DNS services
ii debconf 1.5.82 all Debian configuration management system
ii debian-archive-keyring 2023.3+deb12u1 all GnuPG archive keys of the Debian archive
ii debianutils 5.7-0.5~deb12u1 amd64 Miscellaneous utilities specific to Debian
ii dialog 1.3-20230209-1 amd64 Displays user-friendly dialog boxes from shell scripts
ii diffutils 1:3.8-4 amd64 File comparison utilities
ii dirmngr 2.2.40-1.1 amd64 GNU privacy guard - network certificate management service
ii distro-info-data 0.58+deb12u2 all information about the distributions' releases (data files)
ii dmidecode 3.4-1 amd64 SMBIOS/DMI table decoder
ii dmsetup 2:1.02.185-2 amd64 Linux Kernel Device Mapper userspace library
ii dns-root-data 2024041801~deb12u1 all DNS root hints and DNSSEC trust anchor
ii dnsdist 1.7.3-2 amd64 DNS loadbalancer
ii dnsutils 1:9.18.28-1~deb12u2 all Transitional package for bind9-dnsutils
ii dosfstools 4.2-1 amd64 utilities for making and checking MS-DOS FAT filesystems
ii dpkg 1.21.22 amd64 Debian package management system
ii dropbear 2022.83-1+deb12u1 all lightweight SSH2 server and client - startup scripts
ii dropbear-bin 2022.83-1+deb12u1 amd64 lightweight SSH2 server and client - command line tools
ii e2fsprogs 1.47.0-2 amd64 ext2/ext3/ext4 file system utilities
ii easy-rsa 3.1.0-1 all Simple shell based CA utility
ii efibootmgr 17-2 amd64 Interact with the EFI Boot Manager
ii etherwake 1.09-4+b1 amd64 tool to send magic Wake-on-LAN packets
ii ethtool 1:6.6-1 amd64 display or change Ethernet device settings
ii exfat-fuse 1.3.0+git20220115-2 amd64 read and write exFAT driver for FUSE
ii exfatprogs 1.2.0-1+deb12u1 amd64 exFAT file system utilities
ii fancontrol 1:3.6.0-7.1 all utility to control the fan speed
ii fastnetmon 1.2.4-2 amd64 fast DDoS analyzer with sflow/netflow/mirror support (community edition)
ii fdisk 2.38.1-5+deb12u1 amd64 collection of partitioning utilities
ii file 1:5.44-3 amd64 Recognize the type of data in a file using "magic" numbers
ii findutils 4.9.0-4 amd64 utilities for finding files--find, xargs
ii frr 9.1.1-28-g52b95312f amd64 FRRouting suite of internet protocols (BGP, OSPF, IS-IS, ...)
ii frr-pythontools 9.1.1-28-g52b95312f all FRRouting suite - Python tools
ii frr-rpki-rtrlib 9.1.1-28-g52b95312f amd64 FRRouting suite - BGP RPKI support (rtrlib)
ii frr-snmp 9.1.1-28-g52b95312f amd64 FRRouting suite - SNMP support
ii fuse-overlayfs 1.10-1 amd64 implementation of overlay+shiftfs in FUSE for rootless containers
ii fuse3 3.14.0-4 amd64 Filesystem in Userspace (3.x version)
ii gawk 1:5.2.1-2 amd64 GNU awk, a pattern scanning and processing language
ii gcc-12-base:amd64 12.2.0-14 amd64 GCC, the GNU Compiler Collection (base package)
ii gdisk 1.0.9-2.1 amd64 GPT fdisk text-mode partitioning tool
ii gettext-base 0.21-12 amd64 GNU Internationalization utilities for the base system
ii gir1.2-glib-2.0:amd64 1.74.0-3 amd64 Introspection data for GLib, GObject, Gio and GModule
ii git 1:2.39.2-1.1 amd64 fast, scalable, distributed revision control system
ii git-man 1:2.39.2-1.1 all fast, scalable, distributed revision control system (manual pages)
ii gnupg 2.2.40-1.1 all GNU privacy guard - a free PGP replacement
ii gnupg-l10n 2.2.40-1.1 all GNU privacy guard - localization files
ii gnupg-utils 2.2.40-1.1 amd64 GNU privacy guard - utility programs
ii gnupg2 2.2.40-1.1 all GNU privacy guard - a free PGP replacement (dummy transitional package)
ii gpg 2.2.40-1.1 amd64 GNU Privacy Guard -- minimalist public key operations
ii gpg-agent 2.2.40-1.1 amd64 GNU privacy guard - cryptographic agent
ii gpg-wks-client 2.2.40-1.1 amd64 GNU privacy guard - Web Key Service client
ii gpg-wks-server 2.2.40-1.1 amd64 GNU privacy guard - Web Key Service server
ii gpgconf 2.2.40-1.1 amd64 GNU privacy guard - core configuration utilities
ii gpgsm 2.2.40-1.1 amd64 GNU privacy guard - S/MIME version
ii gpgv 2.2.40-1.1 amd64 GNU privacy guard - signature verification tool
ii grc 1.13.1-1 all generic colouriser for everything
ii grep 3.8-5 amd64 GNU grep, egrep and fgrep
ii grepcidr 2.0-2 amd64 Filter IP addresses matching IPv4/IPv6 CIDR/network specification
ii grub-common 2.06-13+deb12u1 amd64 GRand Unified Bootloader (common files)
ii grub-efi-amd64-bin 2.06-13+deb12u1 amd64 GRand Unified Bootloader, version 2 (EFI-AMD64 modules)
ii grub-pc 2.06-13+deb12u1 amd64 GRand Unified Bootloader, version 2 (PC/BIOS version)
ii grub-pc-bin 2.06-13+deb12u1 amd64 GRand Unified Bootloader, version 2 (PC/BIOS modules)
ii grub2 2.06-13+deb12u1 amd64 GRand Unified Bootloader, version 2 (dummy package)
ii grub2-common 2.06-13+deb12u1 amd64 GRand Unified Bootloader (common files for version 2)
ii gzip 1.12-1 amd64 GNU compression utilities
ii haproxy 2.6.12-1+deb12u1 amd64 fast and reliable load balancing reverse proxy
ii haveged 1.9.14-1+b1 amd64 Linux entropy source using the HAVEGE algorithm
ii hostapd 2.10-2290-ge7172e26d amd64 access point and authentication server for Wi-Fi and Ethernet
ii hostname 3.23+nmu1 amd64 utility to set/show the host name or domain name
ii hsflowd 2.0.55-1 all sFlow(R) monitoring agent
ii htop 3.2.2-2 amd64 interactive processes viewer
ii hvinfo 1.2.0 amd64 x86 hypervisor detection tool
ii hyperv-daemons 6.1.99-1 amd64 Support daemons for Linux running on Hyper-V
ii ieee-data 20220827.1 all OUI and IAB listings
ii iftop 1.0~pre4-9 amd64 displays bandwidth usage information on an network interface
ii igmpproxy 0.3-1 amd64 IGMP multicast routing daemon
ii inetutils-telnet 2:2.4-2+deb12u1 amd64 telnet client
ii init-system-helpers 1.65.2 all helper tools for all init systems
ii initramfs-tools 0.142 all generic modular initramfs generator (automation)
ii initramfs-tools-core 0.142 all generic modular initramfs generator (core tools)
ii iotop 0.6-42-ga14256a-0.1+b2 amd64 simple top-like I/O monitor
ii ipaddrcheck 1.2 amd64 IPv4 and IPv6 address validation utility
ii ipcalc 0.42-2 all parameter calculator for IPv4 addresses
ii iperf 2.1.8+dfsg-1 amd64 Internet Protocol bandwidth measuring tool
ii iperf3 3.12-1+deb12u1 amd64 Internet Protocol bandwidth measuring tool
ii iproute2 6.9.0-1~bpo12+1 amd64 networking and traffic control tools
ii iptables 1.8.9-2 amd64 administration tools for packet filtering and NAT
ii iputils-arping 3:20221126-1 amd64 Tool to send ICMP echo requests to an ARP address
ii iputils-ping 3:20221126-1 amd64 Tools to test the reachability of network hosts
ii ipvsadm 1:1.31-1+b1 amd64 Linux Virtual Server support programs
ii irqtop 2.6-4 all Observe IRQ and SoftIRQ in a top-like fashion
ii isc-dhcp-client 4.4.3-P1-4 amd64 DHCP client for automatically obtaining an IP address
ii isc-dhcp-relay 4.4.3-P1-4 amd64 ISC DHCP relay daemon
ii iw 5.19-1 amd64 tool for configuring Linux wireless devices
ii jool 4.1.9+bf4c7e3669-1 amd64 auto-generated package by debmake
ii jq 1.6-2.1 amd64 lightweight and flexible command-line JSON processor
ii kbd 2.5.1-1+b1 amd64 Linux console font and keytable utilities
ii kea 2.4.1-1 all DHCP server [meta]
ii kea-admin 2.4.1-1 amd64 Administration utilities for Kea DHCP server
ii kea-common 2.4.1-1 amd64 Common libraries for the Kea DHCP server
ii kea-ctrl-agent 2.4.1-1 amd64 REST API service for Kea DHCP server
ii kea-dhcp-ddns-server 2.4.1-1 amd64 DHCP Dynamic DNS service
ii kea-dhcp4-server 2.4.1-1 amd64 IPv4 DHCP server
ii kea-dhcp6-server 2.4.1-1 amd64 IPv6 DHCP server
ii keepalived 1:2.2.8-1 amd64 Failover and monitoring daemon for LVS clusters
ii kitty-terminfo 0.26.5-5 all fast, featureful, GPU based terminal emulator (terminfo file)
ii klibc-utils 2.0.12-1 amd64 small utilities built with klibc for early boot
ii kmod 30+20221128-1 amd64 tools for managing Linux kernel modules
ii lcdproc 0.5.9-6+b2 amd64 LCD display driver daemon and clients
ii lcdproc-extra-drivers:amd64 0.5.9-6+b2 amd64 extra drivers for the LCD display driver daemon
ii less 590-2.1~deb12u2 amd64 pager program similar to more
ii libabsl20220623:amd64 20220623.1-1 amd64 extensions to the C++ standard library
ii libacl1:amd64 2.3.1-3 amd64 access control list - shared library
ii libapp-cmd-perl 0.335-1 all Perl interface to write command line apps with less suffering
ii libapparmor1:amd64 3.0.8-3 amd64 changehat AppArmor library
ii libapt-pkg6.0:amd64 2.6.1 amd64 package management runtime library
ii libargon2-1:amd64 0~20171227-0.3+deb12u1 amd64 memory-hard hashing function - runtime library
ii libassuan0:amd64 2.5.5-5 amd64 IPC library for the GnuPG components
ii libattr1:amd64 1:2.5.1-4 amd64 extended attribute handling - shared library
ii libaudit-common 1:3.0.9-1 all Dynamic library for security auditing - common files
ii libaudit1:amd64 1:3.0.9-1 amd64 Dynamic library for security auditing
ii libauparse0:amd64 1:3.0.9-1 amd64 Dynamic library for parsing security auditing
ii libavahi-common-data:amd64 0.8-10 amd64 Avahi common data files
ii libavahi-common3:amd64 0.8-10 amd64 Avahi common library
ii libavahi-core7:amd64 0.8-10 amd64 Avahi's embeddable mDNS/DNS-SD library
ii libb-hooks-op-check-perl:amd64 0.22-2+b1 amd64 Perl wrapper for OP check callbacks
ii libblas3:amd64 3.11.0-2 amd64 Basic Linear Algebra Reference implementations, shared library
ii libblkid1:amd64 2.38.1-5+deb12u1 amd64 block device ID library
ii libboolean-perl 0.46-3 all module providing transparent support for booleans
ii libboost-context1.74.0:amd64 1.74.0+ds1-21 amd64 provides a sort of cooperative multitasking on a single thread
ii libboost-filesystem1.74.0:amd64 1.74.0+ds1-21 amd64 filesystem operations (portable paths, iteration over directories, etc) in C++
ii libboost-iostreams1.74.0:amd64 1.74.0+ds1-21 amd64 Boost.Iostreams Library
ii libboost-program-options1.74.0:amd64 1.74.0+ds1-21 amd64 program options library for C++
ii libboost-regex1.74.0:amd64 1.74.0+ds1-21 amd64 regular expression library for C++
ii libboost-thread1.74.0:amd64 1.74.0+ds1-21 amd64 portable C++ multi-threading
ii libbpf1:amd64 1:1.1.0-1 amd64 eBPF helper library (shared library)
ii libbrotli1:amd64 1.0.9-2+b6 amd64 library implementing brotli encoder and decoder (shared libraries)
ii libbsd0:amd64 0.11.7-2 amd64 utility functions from BSD systems - shared library
ii libbson-1.0-0 1.23.1-1+b1 amd64 Library to parse and generate BSON documents - runtime files
ii libbz2-1.0:amd64 1.0.8-5+b1 amd64 high-quality block-sorting file compressor library - runtime
ii libc-ares2:amd64 1.18.1-3 amd64 asynchronous name resolver
ii libc-bin 2.36-9+deb12u7 amd64 GNU C Library: Binaries
ii libc-l10n 2.36-9+deb12u7 all GNU C Library: localization files
ii libc6:amd64 2.36-9+deb12u7 amd64 GNU C Library: Shared libraries
ii libcap-ng0:amd64 0.8.3-1+b3 amd64 alternate POSIX capabilities library
ii libcap2:amd64 1:2.66-4 amd64 POSIX 1003.1e capabilities (library)
ii libcap2-bin 1:2.66-4 amd64 POSIX 1003.1e capabilities (utilities)
ii libcapnp-0.9.2:amd64 0.9.2-2 amd64 Cap'n Proto C++ library
ii libcapture-tiny-perl 0.48-2 all module to capture STDOUT and STDERR
ii libcarp-assert-more-perl 2.2.0-1 all set of convenient assertions easier to use than libcarp-assert-perl
ii libcbor0.8:amd64 0.8.0-2+b1 amd64 library for parsing and generating CBOR (RFC 7049)
ii libcdb1:amd64 0.78+b1 amd64 shared library for constant databases (cdb)
ii libcharon-extauth-plugins 5.9.11-2+vyos0 amd64 strongSwan charon library (extended authentication plugins)
ii libcharon-extra-plugins 5.9.11-2+vyos0 amd64 strongSwan charon library (extra plugins)
ii libcidr0:amd64 1.2.3-3 amd64 IP addresses and netblocks manipulation library
ii libclass-data-inheritable-perl 0.08-3 all Perl module to create accessors to class data
ii libclass-load-perl 0.25-2 all module for loading modules by name
ii libclone-choose-perl 0.010-2 all Choose appropriate clone utility (Perl library)
ii libcom-err2:amd64 1.47.0-2 amd64 common error description library
ii libconfig-model-lcdproc-perl 2.053-2 all module to edit and validate LcdProc configuration file
ii libconfig-model-perl 2.152-1 all module for describing and editing configuration data
ii libconfuse-common 3.3-3 all Common files for libConfuse
ii libconfuse2:amd64 3.3-3 amd64 Library for parsing configuration files
ii libcpupower1 6.1.99-1 amd64 CPU frequency and voltage scaling tools for Linux (libraries)
ii libcrypt1:amd64 1:4.4.33-2 amd64 libcrypt shared library
ii libcryptsetup12:amd64 2:2.6.1-4~deb12u2 amd64 disk encryption support - shared library
ii libcurl3-gnutls:amd64 7.88.1-10+deb12u6 amd64 easy-to-use client-side URL transfer library (GnuTLS flavour)
ii libcurl4:amd64 7.88.1-10+deb12u6 amd64 easy-to-use client-side URL transfer library (OpenSSL flavour)
ii libcwidget4:amd64 0.5.18-6 amd64 high-level terminal interface library for C++ (runtime files)
ii libdaemon0:amd64 0.14-7.1 amd64 lightweight C library for daemons - runtime library
ii libdata-optlist-perl 0.113-1 all module to parse and validate simple name/value option pairs
ii libdb5.3:amd64 5.3.28+dfsg2-1 amd64 Berkeley v5.3 Database Libraries [runtime]
ii libdbi-perl:amd64 1.643-4 amd64 Perl Database Interface (DBI)
ii libdbus-1-3:amd64 1.14.10-1~deb12u1 amd64 simple interprocess messaging system (library)
ii libdebconfclient0:amd64 0.270 amd64 Debian Configuration Management System (C-implementation library)
ii libdevel-callchecker-perl:amd64 0.008-2 amd64 custom op checking attached to subroutines
ii libdevel-stacktrace-perl 2.0400-2 all Perl module containing stack trace and related objects
ii libdevmapper1.02.1:amd64 2:1.02.185-2 amd64 Linux Kernel Device Mapper userspace library
ii libdpkg-perl 1.21.22 all Dpkg perl modules
ii libdrm-common 2.4.114-1 all Userspace interface to kernel DRM services -- common files
ii libdrm2:amd64 2.4.114-1+b1 amd64 Userspace interface to kernel DRM services -- runtime
ii libduktape207:amd64 2.7.0-2 amd64 embeddable Javascript engine, library
ii libdynaloader-functions-perl 0.003-3 all deconstructed dynamic C library loading
ii libecap3:amd64 1.0.1-3.4 amd64 eCAP library
ii libedit2:amd64 3.1-20221030-2 amd64 BSD editline and history libraries
ii libefiboot1:amd64 37-6 amd64 Library to manage UEFI variables
ii libefivar1:amd64 37-6 amd64 Library to manage UEFI variables
ii libelf1:amd64 0.188-2.1 amd64 library to read and write ELF files
ii liberror-perl 0.17029-2 all Perl module for error/exception handling in an OO-ish way
ii libestr0:amd64 0.1.11-1 amd64 Helper functions for handling strings (lib)
ii libev4:amd64 1:4.33-1 amd64 high-performance event loop library modelled after libevent
ii libevent-2.1-7:amd64 2.1.12-stable-8 amd64 Asynchronous event notification library
ii libevent-core-2.1-7:amd64 2.1.12-stable-8 amd64 Asynchronous event notification library (core)
ii libevent-pthreads-2.1-7:amd64 2.1.12-stable-8 amd64 Asynchronous event notification library (pthreads)
ii libexception-class-perl 1.45-1 all module that allows you to declare real exception classes in Perl
ii libexpat1:amd64 2.5.0-1 amd64 XML parsing C library - runtime library
ii libexporter-tiny-perl 1.006000-1 all tiny exporter similar to Sub::Exporter
ii libext2fs2:amd64 1.47.0-2 amd64 ext2/ext3/ext4 file system libraries
ii libfastjson4:amd64 1.2304.0-1 amd64 fast json library for C
ii libfdisk1:amd64 2.38.1-5+deb12u1 amd64 fdisk partitioning library
ii libffi8:amd64 3.4.4-1 amd64 Foreign Function Interface library runtime
ii libfido2-1:amd64 1.12.0-2+b1 amd64 library for generating and verifying FIDO 2.0 objects
ii libfile-find-rule-perl 0.34-3 all module to search for files based on rules
ii libfile-homedir-perl 1.006-2 all Perl module for finding user directories across platforms
ii libfile-which-perl 1.27-2 all Perl module for searching paths for executable programs
ii libfreetype6:amd64 2.12.1+dfsg-5+deb12u3 amd64 FreeType 2 font engine, shared library files
ii libfstrm0:amd64 0.6.1-1 amd64 Frame Streams (fstrm) library
ii libfuse2:amd64 2.9.9-6+b1 amd64 Filesystem in Userspace (library)
ii libfuse3-3:amd64 3.14.0-4 amd64 Filesystem in Userspace (library) (3.x version)
ii libgc1:amd64 1:8.2.2-3 amd64 conservative garbage collector for C and C++
ii libgcc-s1:amd64 12.2.0-14 amd64 GCC support library
ii libgcrypt20:amd64 1.10.1-3 amd64 LGPL Crypto library - runtime library
ii libgdbm-compat4:amd64 1.23-3 amd64 GNU dbm database routines (legacy support runtime version)
ii libgdbm6:amd64 1.23-3 amd64 GNU dbm database routines (runtime version)
ii libgetopt-long-descriptive-perl 0.111-1 all module that handles command-line arguments with usage text
ii libgirepository-1.0-1:amd64 1.74.0-3 amd64 Library for handling GObject introspection data (runtime library)
ii libglib2.0-0:amd64 2.74.6-2+deb12u3 amd64 GLib library of C routines
ii libgmp10:amd64 2:6.2.1+dfsg1-1.1 amd64 Multiprecision arithmetic library
ii libgnat-12:amd64 12.2.0-14 amd64 runtime for applications compiled with GNAT (shared library)
ii libgnutls30:amd64 3.7.9-2+deb12u3 amd64 GNU TLS library - main runtime library
ii libgpg-error0:amd64 1.46-1 amd64 GnuPG development runtime library
ii libgpgme11:amd64 1.18.0-3+b1 amd64 GPGME - GnuPG Made Easy (library)
ii libgrpc++1.51:amd64 1.51.1-3+b1 amd64 high performance general RPC framework
ii libgrpc29:amd64 1.51.1-3+b1 amd64 high performance general RPC framework
ii libgssapi-krb5-2:amd64 1.20.1-2+deb12u2 amd64 MIT Kerberos runtime libraries - krb5 GSS-API Mechanism
ii libgudev-1.0-0:amd64 237-2 amd64 GObject-based wrapper library for libudev
ii libh2o-evloop0.13:amd64 2.2.5+dfsg2-7 amd64 H2O library compiled with its own event loop
ii libhash-merge-perl 0.302-1 all Perl module for merging arbitrarily deep hashes into a single hash
ii libhavege2:amd64 1.9.14-1+b1 amd64 entropy source using the HAVEGE algorithm - shared library
ii libhiredis0.14:amd64 0.14.1-3 amd64 minimalistic C client library for Redis
ii libhogweed6:amd64 3.8.1-2 amd64 low level cryptographic library (public-key cryptos)
ii libhtp2 1:0.5.42-1 amd64 HTTP normalizer and parser library
ii libhttp-parser2.9:amd64 2.9.4-5 amd64 parser for HTTP messages written in C
ii libhyperscan5 5.4.0-2 amd64 High-performance regular expression matching library
ii libicu72:amd64 72.1-3 amd64 International Components for Unicode
ii libidn2-0:amd64 2.3.3-1+b1 amd64 Internationalized domain names (IDNA2008/TR46) library
ii libio-stringy-perl 2.111-3 all modules for I/O on in-core objects (strings/arrays)
ii libio-tiecombine-perl 1.005-3 all Perl module to collect output via any kind of tied variable
ii libip4tc2:amd64 1.8.9-2 amd64 netfilter libip4tc library
ii libip6tc2:amd64 1.8.9-2 amd64 netfilter libip6tc library
ii libiperf0:amd64 3.12-1+deb12u1 amd64 Internet Protocol bandwidth measuring tool (runtime files)
ii libjansson4:amd64 2.14-2 amd64 C library for encoding, decoding and manipulating JSON data
ii libjemalloc2:amd64 5.3.0-1 amd64 general-purpose scalable concurrent malloc(3) implementation
ii libjim0.81:amd64 0.81+dfsg0-2 amd64 small-footprint implementation of Tcl - shared library
ii libjq1:amd64 1.6-2.1 amd64 lightweight and flexible command-line JSON processor - shared library
ii libjson-c5:amd64 0.16-2 amd64 JSON manipulation library - shared library
ii libjson-perl 4.10000-1 all module for manipulating JSON-formatted data
ii libk5crypto3:amd64 1.20.1-2+deb12u2 amd64 MIT Kerberos runtime libraries - Crypto Library
ii libkeyutils1:amd64 1.6.3-2 amd64 Linux Key Management Utilities (library)
ii libklibc:amd64 2.0.12-1 amd64 minimal libc subset for use with initramfs
ii libkmod2:amd64 30+20221128-1 amd64 libkmod shared library
ii libkrb5-3:amd64 1.20.1-2+deb12u2 amd64 MIT Kerberos runtime libraries
ii libkrb5support0:amd64 1.20.1-2+deb12u2 amd64 MIT Kerberos runtime libraries - Support library
ii libksba8:amd64 1.6.3-2 amd64 X.509 and CMS support library
ii libldap-2.5-0:amd64 2.5.13+dfsg-5 amd64 OpenLDAP libraries
ii liblinear4:amd64 2.3.0+dfsg-5 amd64 Library for Large Linear Classification
ii liblirc-client0:amd64 0.10.1-7.2 amd64 infra-red remote control support - client library
ii liblist-moreutils-perl 0.430-2 all Perl module with additional list functions not found in List::Util
ii liblist-moreutils-xs-perl 0.430-3+b1 amd64 Perl module providing compiled List::MoreUtils functions
ii liblmdb0:amd64 0.9.24-1 amd64 Lightning Memory-Mapped Database shared library
ii liblog-log4perl-perl 1.57-1 all Perl port of the widely popular log4j logging package
ii liblog4cplus-2.0.5:amd64 2.0.8-1 amd64 C++ logging API modeled after the Java log4j API - shared library
ii liblog4cpp5v5:amd64 1.1.3-3.1+b1 amd64 C++ library for flexible logging (runtime)
ii liblognorm5:amd64 2.0.6-4 amd64 log normalizing library
ii libltdl7:amd64 2.4.7-7~deb12u1 amd64 System independent dlopen wrapper for GNU libtool
ii liblua5.3-0:amd64 5.3.6-2 amd64 Shared library for the Lua interpreter version 5.3
ii libluajit-5.1-2:amd64 2.1.0~beta3+git20220320+dfsg-4.1 amd64 Just in time compiler for Lua - library version
ii libluajit-5.1-common 2.1.0~beta3+git20220320+dfsg-4.1 all Just in time compiler for Lua - common files
ii liblz4-1:amd64 1.9.4-1 amd64 Fast LZ compression algorithm library - runtime
ii liblzma5:amd64 5.4.1-0.2 amd64 XZ-format compression library
ii liblzo2-2:amd64 2.10-2 amd64 data compression library
ii libmagic-mgc 1:5.44-3 amd64 File type determination library using "magic" numbers (compiled magic file)
ii libmagic1:amd64 1:5.44-3 amd64 Recognize the type of data in a file using "magic" numbers - library
ii libmariadb3:amd64 1:10.11.6-0+deb12u1 amd64 MariaDB database client library
ii libmaxminddb0:amd64 1.7.1-1 amd64 IP geolocation database library
ii libmbim-glib4:amd64 1.28.2-1 amd64 Support library to use the MBIM protocol
ii libmbim-proxy 1.28.2-1 amd64 Proxy to communicate with MBIM ports
ii libmd0:amd64 1.0.4-2 amd64 message digest functions from BSD systems - shared library
ii libmm-glib0:amd64 1.20.4-1 amd64 D-Bus service for managing modems - shared libraries
ii libmnl0:amd64 1.0.4-3 amd64 minimalistic Netlink communication library
ii libmodule-implementation-perl 0.09-2 all module for loading one of several alternate implementations of a module
ii libmodule-pluggable-perl 5.2-4 all module for giving modules the ability to have plugins
ii libmodule-runtime-perl 0.016-2 all Perl module for runtime module handling
ii libmongoc-1.0-0 1.23.1-1+b1 amd64 MongoDB C client library - runtime files
ii libmongocrypt0:amd64 1.7.2-1 amd64 client-side field level encryption library - runtime files
ii libmount1:amd64 2.38.1-5+deb12u1 amd64 device mounting library
ii libmouse-perl 2.5.10-1+b3 amd64 lightweight object framework for Perl
ii libmousex-nativetraits-perl 1.09-3 all extension for attribute interfaces for Mouse
ii libmousex-strictconstructor-perl 0.02-3 all Mouse extension for making object constructors die on unknown attributes
ii libmpfr6:amd64 4.2.0-1 amd64 multiple precision floating-point computation
ii libmspack0:amd64 0.11-1 amd64 library for Microsoft compression formats (shared library)
ii libncurses6:amd64 6.4-4 amd64 shared libraries for terminal handling
ii libncursesw6:amd64 6.4-4 amd64 shared libraries for terminal handling (wide character support)
ii libndp-tools 1.8-1+deb12u1 amd64 Library for Neighbor Discovery Protocol (tools)
ii libndp0:amd64 1.8-1+deb12u1 amd64 Library for Neighbor Discovery Protocol
ii libnet1:amd64 1.1.6+dfsg-3.2 amd64 library for the construction and handling of network packets
ii libnetfilter-conntrack3:amd64 1.0.9-1 amd64 Netfilter netlink-conntrack library
ii libnetfilter-cthelper0:amd64 1.0.1-1 amd64 userspace-helper for netfilter library
ii libnetfilter-cttimeout1:amd64 1.0.1-1 amd64 fine-grain connection tracking timeout infrastructure for netfilter
ii libnetfilter-log1:amd64 1.0.2-3 amd64 Netfilter netlink-log library
ii libnetfilter-queue1:amd64 1.0.5-3 amd64 Netfilter netlink-queue library
ii libnettle8:amd64 3.8.1-2 amd64 low level cryptographic library (symmetric and one-way cryptos)
ii libnfnetlink0:amd64 1.0.2-2 amd64 Netfilter netlink library
ii libnftables1:amd64 1.0.9-1 amd64 Netfilter nftables high level userspace API library
ii libnftnl11:amd64 1.2.6-2 amd64 Netfilter nftables userspace API library
ii libnghttp2-14:amd64 1.52.0-1+deb12u1 amd64 library implementing HTTP/2 protocol (shared library)
ii libnginx-mod-http-echo 1:0.63-4 amd64 Bring echo and more shell style goodies to Nginx
ii libnl-3-200:amd64 3.7.0-0.2+b1 amd64 library for dealing with netlink sockets
ii libnl-genl-3-200:amd64 3.7.0-0.2+b1 amd64 library for dealing with netlink sockets - generic netlink
ii libnl-route-3-200:amd64 3.7.0-0.2+b1 amd64 library for dealing with netlink sockets - route interface
ii libnorm1:amd64 1.5.9+dfsg-2 amd64 NACK-Oriented Reliable Multicast (NORM) library
ii libnpth0:amd64 1.6-3 amd64 replacement for GNU Pth using system threads
ii libnsl2:amd64 1.3.0-2 amd64 Public client interface for NIS(YP) and NIS+
ii libnspr4:amd64 2:4.35-1 amd64 NetScape Portable Runtime Library
ii libnss-mapuser 1.1.0-cl3u3 amd64 NSS modules to map any requested username to a local account
ii libnss-myhostname:amd64 252.26-1~deb12u2 amd64 nss module providing fallback resolution for the current hostname
ii libnss-tacplus 1.0.4-cl5.1.0u11 amd64 NSS module for TACACS+ authentication without local passwd entry
ii libnss3:amd64 2:3.87.1-1 amd64 Network Security Service libraries
ii libnuma1:amd64 2.0.16-1 amd64 Libraries for controlling NUMA policy
ii libnumber-compare-perl 0.03-3 all module for performing numeric comparisons in Perl
ii libnvme1 1.3-1 amd64 NVMe management library (library)
ii liboath0:amd64 2.6.7-3.1 amd64 OATH Toolkit Liboath library
ii libobjc4:amd64 12.2.0-14 amd64 Runtime library for GNU Objective-C applications
ii libonig5:amd64 6.9.8-1 amd64 regular expressions library
ii libopentracing-c-wrapper0:amd64 1.1.3-3+b1 amd64 C wrapper for the C++ impl of the OpenTracing API
ii libopentracing1:amd64 1.6.0-4 amd64 OpenTracing API for C++
ii libp11-kit0:amd64 0.24.1-2 amd64 library for loading and coordinating access to PKCS#11 modules - runtime
ii libpackage-stash-perl 0.40-1 all module providing routines for manipulating stashes
ii libpam-cap:amd64 1:2.66-4 amd64 POSIX 1003.1e capabilities (PAM module)
ii libpam-google-authenticator 20191231-2 amd64 Two-step verification
ii libpam-modules:amd64 1.5.2-6+deb12u1 amd64 Pluggable Authentication Modules for PAM
ii libpam-modules-bin 1.5.2-6+deb12u1 amd64 Pluggable Authentication Modules for PAM - helper binaries
ii libpam-radius-auth 1.5.0-cl3u7 amd64 PAM RADIUS client authentication module
ii libpam-runtime 1.5.2-6+deb12u1 all Runtime support for the PAM library
ii libpam-systemd:amd64 252.26-1~deb12u2 amd64 system and service manager - PAM module
ii libpam-tacplus 1.4.3-cl5.1.0u5 amd64 PAM module for using TACACS+ as an authentication service
ii libpam0g:amd64 1.5.2-6+deb12u1 amd64 Pluggable Authentication Modules library
ii libparams-classify-perl:amd64 0.015-2+b1 amd64 Perl module for argument type classification
ii libparams-util-perl 1.102-2+b1 amd64 Perl extension for simple stand-alone param checking functions
ii libparams-validate-perl:amd64 1.31-1 amd64 Perl module to validate parameters to Perl method/function calls
ii libparse-recdescent-perl 1.967015+dfsg-4 all Perl module to create and use recursive-descent parsers
ii libparted2:amd64 3.5-3 amd64 disk partition manipulator - shared library
ii libpath-tiny-perl 0.144-1 all file path utility
ii libpcap0.8:amd64 1.10.3-1 amd64 system interface for user-level packet capture
ii libpci3:amd64 1:3.9.0-4 amd64 PCI utilities (shared library)
ii libpcre2-8-0:amd64 10.42-1 amd64 New Perl Compatible Regular Expression Library- 8 bit runtime files
ii libpcre3:amd64 2:8.39-15 amd64 Old Perl 5 Compatible Regular Expression Library - runtime files
ii libpcsclite1:amd64 1.9.9-2 amd64 Middleware to access a smart card using PC/SC (library)
ii libperl5.36:amd64 5.36.0-7+deb12u1 amd64 shared Perl library
ii libpgm-5.3-0:amd64 5.3.128~dfsg-2 amd64 OpenPGM shared library
ii libpkcs11-helper1:amd64 1.29.0-1 amd64 library that simplifies the interaction with PKCS#11
ii libpng16-16:amd64 1.6.39-2 amd64 PNG library - runtime (version 1.6)
ii libpod-pom-perl 2.01-4 all module providing a Pod Object Model
ii libpolkit-agent-1-0:amd64 122-3 amd64 polkit Authentication Agent API
ii libpolkit-gobject-1-0:amd64 122-3 amd64 polkit Authorization API
ii libpopt0:amd64 1.19+dfsg-1 amd64 lib for parsing cmdline parameters
ii libpq5:amd64 15.7-0+deb12u1 amd64 PostgreSQL C client library
ii libproc2-0:amd64 2:4.0.2-3 amd64 library for accessing process information from /proc
ii libprotobuf-c1:amd64 1.4.1-1+b1 amd64 Protocol Buffers C shared library (protobuf-c)
ii libprotobuf32:amd64 3.21.12-3 amd64 protocol buffers C++ library
ii libprotoc32:amd64 3.21.12-3 amd64 protocol buffers compiler library
ii libpsl5:amd64 0.21.2-1 amd64 Library for Public Suffix List (shared libraries)
ii libpython3-stdlib:amd64 3.11.2-1+b1 amd64 interactive high-level object-oriented language (default python3 version)
ii libpython3.11-minimal:amd64 3.11.2-6+deb12u2 amd64 Minimal subset of the Python language (version 3.11)
ii libpython3.11-stdlib:amd64 3.11.2-6+deb12u2 amd64 Interactive high-level object-oriented language (standard library, version 3.11)
ii libqmi-glib5:amd64 1.32.2-1 amd64 Support library to use the Qualcomm MSM Interface (QMI) protocol
ii libqmi-proxy 1.32.2-1 amd64 Proxy to communicate with QMI ports
ii libqmi-utils 1.32.2-1 amd64 Utilities to use the QMI protocol from the command line
ii libqrencode4:amd64 4.1.1-1 amd64 QR Code encoding library
ii libqrtr-glib0:amd64 1.2.2-1 amd64 Support library to use the QRTR protocol
ii librabbitmq4:amd64 0.11.0-1+b1 amd64 AMQP client library written in C
ii libradcli4 1.2.11-1+b2 amd64 Enhanced RADIUS client library
ii librdkafka1:amd64 2.0.2-1 amd64 library implementing the Apache Kafka protocol
ii libre2-9:amd64 20220601+dfsg-1+b1 amd64 efficient, principled regular expression library
ii libreadline8:amd64 8.2-1.3 amd64 GNU readline and history libraries, run-time libraries
ii libregexp-common-perl 2017060201-3 all module with common regular expressions
ii librtmp1:amd64 2.4+20151223.gitfa8646d.1-2+b2 amd64 toolkit for RTMP streams (shared library)
ii librtr0:amd64 0.8.0 amd64 Small extensible RPKI-RTR-Client C library.
ii libruby:amd64 1:3.1 amd64 Libraries necessary to run Ruby
ii libruby3.1:amd64 3.1.2-7+deb12u1 amd64 Libraries necessary to run Ruby 3.1
ii libsasl2-2:amd64 2.1.28+dfsg-10 amd64 Cyrus SASL - authentication abstraction library
ii libsasl2-modules-db:amd64 2.1.28+dfsg-10 amd64 Cyrus SASL - pluggable authentication modules (DB)
ii libsctp1:amd64 1.0.19+dfsg-2 amd64 user-space access to Linux kernel SCTP - shared library
ii libseccomp2:amd64 2.5.4-1+deb12u1 amd64 high level interface to Linux seccomp filter
ii libselinux1:amd64 3.4-1+b6 amd64 SELinux runtime shared libraries
ii libsemanage-common 3.4-1 all Common files for SELinux policy management libraries
ii libsemanage2:amd64 3.4-1+b5 amd64 SELinux policy management library
ii libsensors-config 1:3.6.0-7.1 all lm-sensors configuration files
ii libsensors5:amd64 1:3.6.0-7.1 amd64 library to read temperature/voltage/fan sensors
ii libsepol2:amd64 3.4-2.1 amd64 SELinux library for manipulating binary security policies
ii libsigc++-2.0-0v5:amd64 2.12.0-1 amd64 type-safe Signal Framework for C++ - runtime
ii libsigsegv2:amd64 2.14-1 amd64 Library for handling page faults in a portable way
ii libsmartcols1:amd64 2.38.1-5+deb12u1 amd64 smart column output alignment library
ii libsnappy1v5:amd64 1.1.9-3 amd64 fast compression/decompression library
ii libsnmp-base 5.9.4+dfsg-1 all SNMP configuration script, MIBs and documentation
ii libsnmp40:amd64 5.9.4+dfsg-1 amd64 SNMP (Simple Network Management Protocol) library
ii libsodium23:amd64 1.0.18-1 amd64 Network communication, cryptography and signaturing library
ii libsqlite3-0:amd64 3.40.1-2 amd64 SQLite 3 shared library
ii libss2:amd64 1.47.0-2 amd64 command-line interface parsing library
ii libssh-4:amd64 0.10.6-0+deb12u1 amd64 tiny C SSH library (OpenSSL flavor)
ii libssh2-1:amd64 1.10.0-3+b1 amd64 SSH2 client-side library
ii libssl3:amd64 3.0.13-1~deb12u1 amd64 Secure Sockets Layer toolkit - shared libraries
ii libsstp-api-0 1.0.18-1 amd64 Connect to a Microsoft Windows 2008 server using SSTP VPN
ii libstdc++6:amd64 12.2.0-14 amd64 GNU Standard C++ Library v3
ii libstring-rewriteprefix-perl 0.009-1 all module to rewrite strings based on a set of known prefixes
ii libstrongswan 5.9.11-2+vyos0 amd64 strongSwan utility and crypto library
ii libstrongswan-extra-plugins 5.9.11-2+vyos0 amd64 strongSwan utility and crypto library (extra plugins)
ii libstrongswan-standard-plugins 5.9.11-2+vyos0 amd64 strongSwan utility and crypto library (standard plugins)
ii libsub-exporter-perl 0.989-1 all sophisticated exporter for custom-built routines
ii libsub-install-perl 0.929-1 all module for installing subroutines into packages easily
ii libsub-uplevel-perl 0.2800-3 all module to spoof the Perl call stack
ii libsubid4:amd64 1:4.13+dfsg1-1+b1 amd64 subordinate id handling library -- shared library
ii libsystemd-shared:amd64 252.26-1~deb12u2 amd64 systemd shared private library
ii libsystemd0:amd64 252.26-1~deb12u2 amd64 systemd utility library
ii libtac2 1.4.3-cl5.1.0u5 amd64 TACACS+ protocol library
ii libtacplus-map1 1.0.1-cl5.1.0u9 amd64 Library for mapping TACACS+ users without local /etc/passwd entries
ii libtalloc2:amd64 2.4.0-f2 amd64 hierarchical pool based memory allocator
ii libtasn1-6:amd64 4.19.0-2 amd64 Manage ASN.1 structures (runtime)
ii libtdb1:amd64 1.4.8-2 amd64 Trivial Database - shared library
ii libtest-exception-perl 0.43-3 all module for testing exception-based code
ii libtext-glob-perl 0.11-3 all Perl module for matching globbing patterns against text
ii libtinfo6:amd64 6.4-4 amd64 shared low-level terminfo library for terminal handling
ii libtirpc-common 1.3.3+ds-1 all transport-independent RPC library - common files
ii libtirpc3:amd64 1.3.3+ds-1 amd64 transport-independent RPC library
ii libtomcrypt1:amd64 1.18.2-6 amd64 public domain open source cryptographic toolkit
ii libtommath1:amd64 1.2.0-6+deb12u1 amd64 multiple-precision integer library [runtime]
ii libtry-tiny-perl 0.31-2 all module providing minimalistic try/catch
ii libtss2-esys-3.0.2-0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-fapi1:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-mu0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-rc0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-sys1:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-tcti-cmd0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-tcti-device0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-tcti-mssim0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-tcti-swtpm0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libtss2-tctildr0:amd64 3.2.1-3 amd64 TPM2 Software stack library - TSS and TCTI libraries
ii libudev1:amd64 252.26-1~deb12u2 amd64 libudev shared library
ii libunistring2:amd64 1.0-2 amd64 Unicode string library for C
ii liburing2:amd64 2.3-3 amd64 Linux kernel io_uring access library - shared library
ii libusb-1.0-0:amd64 2:1.0.26-1 amd64 userspace USB programming library
ii libutempter0:amd64 1.2.1-3 amd64 privileged helper for utmp/wtmp updates (runtime)
ii libuuid1:amd64 2.38.1-5+deb12u1 amd64 Universally Unique ID library
ii libuv1:amd64 1.44.2-1+deb12u1 amd64 asynchronous event notification library - runtime library
ii libvyatta-cfg1 0.102.0+vyos2+current5 amd64 vyatta-cfg back-end library
ii libvyosconfig0 0.0.10 amd64 VyConf config tree manipulation library
ii libwrap0:amd64 7.6.q-32 amd64 Wietse Venema's TCP wrappers library
ii libwslay1:amd64 1.1.1-3+b1 amd64 WebSocket library written in C. Shared library
ii libx11-6:amd64 2:1.8.4-2+deb12u2 amd64 X11 client-side library
ii libx11-data 2:1.8.4-2+deb12u2 all X11 client-side library
ii libxapian30:amd64 1.4.22-1 amd64 Search engine library
ii libxau6:amd64 1:1.0.9-1 amd64 X11 authorisation library
ii libxcb1:amd64 1.15-1 amd64 X C Binding
ii libxdmcp6:amd64 1:1.1.2-3 amd64 X11 Display Manager Control Protocol library
ii libxext6:amd64 2:1.3.4-1+b1 amd64 X11 miscellaneous extension library
ii libxinerama1:amd64 2:1.1.4-3 amd64 X11 Xinerama extension library
ii libxml2:amd64 2.9.14+dfsg-1.3~deb12u1 amd64 GNOME XML library
ii libxmlsec1:amd64 1.2.37-2 amd64 XML security library
ii libxmlsec1-openssl:amd64 1.2.37-2 amd64 Openssl engine for the XML security library
ii libxosd2 2.2.14-2.1+b1 amd64 X On-Screen Display library - runtime
ii libxslt1.1:amd64 1.1.35-1 amd64 XSLT 1.0 processing library - runtime library
ii libxtables12:amd64 1.8.9-2 amd64 netfilter xtables library
ii libxxhash0:amd64 0.8.1-1 amd64 shared library for xxhash
ii libyajl2:amd64 2.1.0-3+deb12u2 amd64 Yet Another JSON Library
ii libyaml-0-2:amd64 0.2.5-1 amd64 Fast YAML 1.1 parser and emitter library
ii libyaml-pp-perl 0.035-1 all pure-perl YAML framework
ii libyaml-tiny-perl 1.73-1 all Perl module for reading and writing YAML files
ii libyang2:amd64 2.1.148-1 amd64 parser toolkit for IETF YANG data modeling - runtime
ii libzmq5:amd64 4.3.4-6 amd64 lightweight messaging kernel (shared library)
ii libzstd1:amd64 1.5.4+dfsg2-5 amd64 fast lossless compression algorithm
ii linux-base 4.9 all Linux image base package
ii linux-cpupower 6.1.99-1 amd64 CPU power management tools for Linux
ii linux-image-6.6.43-amd64-vyos 6.6.43-1 amd64 Linux kernel, version 6.6.43-amd64-vyos
ii live-boot 1:20151213-vyos0 all Live System Boot Components
ii live-boot-initramfs-tools 1:20151213-vyos0 all Live System Boot Components (initramfs-tools backend)
ii live-config 11.0.3+nmu1 all Live System Configuration Components
ii live-config-systemd 11.0.3+nmu1 all Live System Configuration Components (systemd backend)
ii lldpd 1.0.16-1+deb12u1 amd64 implementation of IEEE 802.1ab (LLDP)
ii lm-sensors 1:3.6.0-7.1 amd64 utilities to read temperature/voltage/fan sensors
ii localepurge 0.7.3.10 all reclaim disk space by removing unneeded localizations
ii locales 2.36-9+deb12u7 all GNU C Library: National Language (locale) data [support]
ii login 1:4.13+dfsg1-1+b1 amd64 system login tools
ii logrotate 3.21.0-1 amd64 Log rotation utility
ii logsave 1.47.0-2 amd64 save the output of a command in a log file
ii lsb-base 11.6 all transitional package for Linux Standard Base init script functionality
ii lsb-release 12.0-1 all Linux Standard Base version reporting utility (minimal implementation)
ii lsof 4.95.0-1 amd64 utility to list open files
ii lsscsi 0.31-1+b1 amd64 list all SCSI devices (or hosts) currently on system
ii lua-lpeg:amd64 1.0.2-2 amd64 LPeg library for the Lua language
ii mariadb-common 1:10.11.6-0+deb12u1 all MariaDB common configuration files
ii mawk 1.3.4.20200120-3.1 amd64 Pattern scanning and text processing language
ii mdadm 4.2-5 amd64 Tool to administer Linux MD arrays (software RAID)
ii media-types 10.0.0 all List of standard media types and their usual file extension
ii minicom 2.8-2 amd64 Friendly menu driven serial communication program
ii minisign 0.11-1 amd64 Dead simple tool to sign files and verify signatures
ii mlnx-ofed-kernel-modules 24.04.OFED.24.04.0.6.6.1-1.kver.6.6.43-amd64-vyos amd64 mlnx-ofed kernel modules
ii mlnx-ofed-kernel-utils 24.04.OFED.24.04.0.6.6.1-1.kver.6.6.43-amd64-vyos amd64 Userspace tools to restart and tune mlnx-ofed kernel modules
ii mlnx-tools 24.04.0-1.2404066 amd64 Userspace tools to restart and tune MLNX_OFED kernel modules
ii modemmanager 1.20.4-1 amd64 D-Bus service for managing modems
ii mount 2.38.1-5+deb12u1 amd64 tools for mounting and manipulating filesystems
ii mtr-tiny 0.95-1 amd64 Full screen ncurses traceroute tool
ii mysql-common 5.8+1.1.0 all MySQL database common files, e.g. /etc/mysql/my.cnf
ii nano 7.2-1+deb12u1 amd64 small, friendly text editor inspired by Pico
ii nat-rtsp 5.3-2-g475af0a amd64 Connection tracking and NAT support for RTSP
ii ncal 12.1.8 amd64 display a calendar and the date of Easter
ii ncurses-base 6.4-4 all basic terminal type definitions
ii ncurses-bin 6.4-4 amd64 terminal-related programs and man pages
ii ncurses-term 6.4-4 all additional terminal type definitions
ii ndisc6 1.0.5-1+b2 amd64 IPv6 diagnostic tools
ii ndppd 0.2.5-6 amd64 daemon that proxies IPv6 NDP messages
ii net-tools 2.10-0.1 amd64 NET-3 networking toolkit
ii netavark 1.4.0-3 amd64 Rust based network stack for containers
ii netbase 6.4 all Basic TCP/IP networking system
ii netcat-openbsd 1.219-1 amd64 TCP/IP swiss army knife
ii netplug 1.2.9.2-3.1 amd64 network link monitor daemon
ii nfct 1:1.4.7-1+b2 amd64 Tool to interact with the connection tracking system
ii nftables 1.0.9-1 amd64 Program to control packet filtering rules by Netfilter project
ii nginx 1.22.1-9 amd64 small, powerful, scalable web/proxy server
ii nginx-common 1.22.1-9 all small, powerful, scalable web/proxy server - common files
ii nginx-light 1.22.1-9 all nginx web/proxy server (basic version)
ii nmap 7.93+dfsg1-1 amd64 The Network Mapper
ii nmap-common 7.93+dfsg1-1 all Architecture independent files for nmap
ii numactl 2.0.16-1 amd64 NUMA scheduling and memory placement tool
ii nvme-cli 2.4+really2.3-3 amd64 NVMe management tool
ii ocserv 1.1.6-3 amd64 OpenConnect VPN server compatible with Cisco AnyConnect VPN
ii open-vm-tools 2:12.2.0-1+deb12u2 amd64 Open VMware Tools for virtual machines hosted on VMware (CLI)
ii opennhrp 0.14-20-g613277f amd64 NBMA Next Hop Resolution Protocol daemon
ii openssh-client 1:9.2p1-2+deb12u3 amd64 secure shell (SSH) client, for secure access to remote machines
ii openssh-server 1:9.2p1-2+deb12u3 amd64 secure shell (SSH) server, for secure access from remote machines
ii openssh-sftp-server 1:9.2p1-2+deb12u3 amd64 secure shell (SSH) sftp server module, for SFTP access from remote machines
ii openssl 3.0.13-1~deb12u1 amd64 Secure Sockets Layer toolkit - cryptographic utility
ii openvpn 2.6.3-1+deb12u2 amd64 virtual private network daemon
ii openvpn-auth-ldap 2.0.4-3 amd64 OpenVPN LDAP authentication module
ii openvpn-auth-radius 2.1-8 amd64 OpenVPN RADIUS authentication module
ii openvpn-dco 0.2.20231117 amd64 OpenVPN Data Channel Offload
ii openvpn-otp 1.0-4-g47f8ccf amd64 OpenVPN OTP Authentication support.
ii owamp-client 4.4.6-1 amd64 OWAMP command line client utilities
ii owamp-server 4.4.6-1 amd64 OWAMP daemon
ii parted 3.5-3 amd64 disk partition manipulator
ii passwd 1:4.13+dfsg1-1+b1 amd64 change and administer password and group data
ii pci.ids 0.0~2023.04.11-1 all PCI ID Repository
ii pciutils 1:3.9.0-4 amd64 PCI utilities
ii pdns-recursor 4.8.8-1 amd64 PowerDNS Recursor
ii perl 5.36.0-7+deb12u1 amd64 Larry Wall's Practical Extraction and Report Language
ii perl-base 5.36.0-7+deb12u1 amd64 minimal Perl system
ii perl-modules-5.36 5.36.0-7+deb12u1 all Core Perl modules
ii pinentry-curses 1.2.1-1 amd64 curses-based PIN or pass-phrase entry dialog for GnuPG
ii pmacct 1.7.7-1 amd64 promiscuous mode traffic accountant
ii podman 4.9.5 amd64 Engine to run OCI-based containers in Pods
ii polkitd 122-3 amd64 framework for managing administrative policies and privileges
ii ppp 2.4.9-1+1.1+b1 amd64 Point-to-Point Protocol (PPP) - daemon
ii pppoe 3.15-2 amd64 PPP over Ethernet driver
ii procps 2:4.0.2-3 amd64 /proc file system utilities
ii psmisc 23.6-1 amd64 utilities that use the proc file system
ii publicsuffix 20230209.2326-1 all accurate, machine-readable list of domain name suffixes
ii python-apt-common 2.6.0 all Python interface to libapt-pkg (locales)
ii python3 3.11.2-1+b1 amd64 interactive high-level object-oriented language (default python3 version)
ii python3-acme 2.1.0-1 all ACME protocol library for Python 3
ii python3-apt 2.6.0 amd64 Python 3 interface to libapt-pkg
ii python3-bcrypt 3.2.2-1 amd64 password hashing library for Python 3
ii python3-certbot 2.1.0-4 all main library for certbot
ii python3-certifi 2022.9.24-1 all root certificates for validating SSL certs and verifying TLS hosts (python3)
ii python3-cffi-backend:amd64 1.15.1-5+b1 amd64 Foreign Function Interface for Python 3 calling C code - runtime
ii python3-chardet 5.1.0+dfsg-2 all Universal Character Encoding Detector (Python3)
ii python3-charset-normalizer 3.0.1-2 all charset, encoding and language detection (Python 3)
ii python3-configargparse 1.5.3-1 all replacement for argparse with config files and environment variables (Python 3)
ii python3-configobj 5.0.8-1 all simple but powerful config file reader and writer for Python 3
ii python3-cryptography 38.0.4-3 amd64 Python library exposing cryptographic recipes and primitives (Python 3)
ii python3-dateutil 2.8.2-2 all powerful extensions to the standard Python 3 datetime module
ii python3-dbus 1.3.2-4+b1 amd64 simple interprocess messaging system (Python 3 interface)
ii python3-distro 1.8.0-1 all Linux OS platform information API
ii python3-gi 3.42.2-3+b1 amd64 Python 3 bindings for gobject-introspection libraries
ii python3-hurry.filesize 0.9-3 all human readable file sizes or anything sized in bytes - Python 3.x
ii python3-idna 3.3-1+deb12u1 all Python IDNA2008 (RFC 5891) handling (Python 3)
ii python3-inotify 0.2.10-1 all An adapter to Linux kernel support for inotify directory-wat
ii python3-jinja2 3.1.2-1 all small but fast and easy to use stand-alone template engine
ii python3-jmespath 1.0.1-1 all JSON Matching Expressions (Python 3)
ii python3-josepy 1.13.0-1 all JOSE implementation for Python 3.x
ii python3-kea-connector 2.4.1-1 all Python3 management connector for Kea DHCP server
ii python3-linux-procfs 0.6.3-1.1+b2 amd64 Linux /proc abstraction classes in Python
ii python3-markupsafe 2.1.2-1+b1 amd64 HTML/XHTML/XML string library
ii python3-minimal 3.11.2-1+b1 amd64 minimal subset of the Python language (default python3 version)
ii python3-msgpack 1.0.3-2+b1 amd64 Python 3 implementation of MessagePack format
ii python3-nacl 1.5.0-2 amd64 Python bindings to libsodium (Python 3)
ii python3-netaddr 0.8.0-2 all manipulation of various common network address notations (Python 3)
ii python3-netifaces:amd64 0.11.0-2+b1 amd64 portable network interface information - Python 3.x
ii python3-openssl 23.0.0-1 all Python 3 wrapper around the OpenSSL library
ii python3-paramiko 2.12.0-2 all Make ssh v2 connections (Python 3)
ii python3-parsedatetime 2.6-3 all Python 3 module to parse human-readable date/time expressions
ii python3-passlib 1.7.4-3 all comprehensive password hashing framework
ii python3-pkg-resources 66.1.1-1 all Package Discovery and Resource Access using pkg_resources
ii python3-psutil 5.9.4-1+b1 amd64 module providing convenience functions for managing processes (Python3)
ii python3-py 1.11.0-1 all Advanced Python development support library (Python 3)
ii python3-pycryptodome 3.11.0+dfsg1-4 amd64 cryptographic Python library (Python 3)
ii python3-pyhumps 3.8.0-1 all <F0><9F><90><AB> Convert strings (and dictionary keys) between snake case,
ii python3-pyroute2 0.7.2-2 all Python3 Netlink library - full package
ii python3-pystache 0.6.0-1 all Python3 implementation of Mustache
ii python3-pyudev 0.24.0-1 all Python3 bindings for libudev
ii python3-requests 2.28.1+dfsg-1 all elegant and simple HTTP library for Python3, built for human beings
ii python3-rfc3339 1.1-4 all parser and generator of RFC 3339-compliant timestamps (Python 3)
ii python3-six 1.16.0-4 all Python 2 and 3 compatibility library
ii python3-systemd 235-1+b2 amd64 Python 3 bindings for systemd
ii python3-tabulate 0.8.9-1 all pretty-print tabular data in Python3
ii python3-tz 2022.7.1-4 all Python3 version of the Olson timezone database
ii python3-urllib3 1.26.12-1 all HTTP library with thread-safe connection pooling for Python3
ii python3-vici 5.9.8-1 all Native Python interface for strongSwan's VICI protocol
ii python3-voluptuous 0.12.2-1 all Python 3 library to validate data
ii python3-xmltodict 0.13.0-1 all Makes working with XML feel like you are working with JSON (Python 3)
ii python3-yaml 6.0-3+b2 amd64 YAML parser and emitter for Python3
ii python3-zmq 24.0.1-4+b1 amd64 Python3 bindings for 0MQ library
ii python3.11 3.11.2-6+deb12u2 amd64 Interactive high-level object-oriented language (version 3.11)
ii python3.11-minimal 3.11.2-6+deb12u2 amd64 Minimal subset of the Python language (version 3.11)
ii qemu-guest-agent 1:7.2+dfsg-7+deb12u6 amd64 Guest-side qemu-system agent
ii qrencode 4.1.1-1 amd64 QR Code encoder into PNG image
ii radius-shell 1.5.0-cl3u7 amd64 Shell front-end used for radius users.
ii radvd 2.20-rc1-23-gf2de476 amd64 RADVD router advertisement daemon
ii rake 13.0.6-3 all ruby make-like utility
ii readline-common 8.2-1.3 all GNU readline and history libraries, common files
ii rsync 3.2.7-1 amd64 fast, versatile, remote (and local) file-copying tool
ii rsyslog 8.2302.0-1 amd64 reliable system and kernel logging daemon
ii ruby 1:3.1 amd64 Interpreter of object-oriented scripting language Ruby (default version)
ii ruby-curses 1.4.4-1+b2 amd64 curses binding for Ruby
ii ruby-net-telnet 0.2.0-1 all telnet client library
ii ruby-rubygems 3.3.15-2 all Package management framework for Ruby
ii ruby-sdbm:amd64 1.0.0-5+b1 amd64 simple file-based key-value store with String keys and values
ii ruby-webrick 1.8.1-1 all HTTP server toolkit in Ruby
ii ruby-xmlrpc 0.3.2-2 all XMLRPC library for Ruby
ii ruby3.1 3.1.2-7+deb12u1 amd64 Interpreter of object-oriented scripting language Ruby
ii rubygems-integration 1.18 all integration of Debian Ruby packages with Rubygems
ii runit-helper 2.15.2 all dh-runit implementation detail
ii salt-common 3005.5+ds-1 all shared libraries that salt requires for all packages
ii salt-minion 3005.5+ds-1 all client package for salt, the distributed remote execution system
ii screen 4.9.0-4 amd64 terminal multiplexer with VT100/ANSI terminal emulation
ii sed 4.9-1 amd64 GNU stream editor for filtering/transforming text
ii sensible-utils 0.0.17+nmu1 all Utilities for sensible alternative selection
ii sgml-base 1.31 all SGML infrastructure and SGML catalog file support
ii sharutils 1:4.15.2-9 amd64 shar, unshar, uuencode, uudecode
ii sipcalc 1.1.6-3 amd64 Advanced console-based ip subnet calculator
ii smartmontools 7.3-1+b1 amd64 control and monitor storage systems using S.M.A.R.T.
ii snmp 5.9.4+dfsg-1 amd64 SNMP (Simple Network Management Protocol) applications
ii snmpd 5.9.4+dfsg-1 amd64 SNMP (Simple Network Management Protocol) agents
ii socat 1.7.4.4-2 amd64 multipurpose relay for bidirectional data transfer
ii squashfs-tools 1:4.5.1-1 amd64 Tool to create and append to squashfs filesystems
ii squid 5.7-2+deb12u1 amd64 Full featured Web Proxy cache (HTTP proxy GnuTLS flavour)
ii squid-common 5.7-2+deb12u1 all Full featured Web Proxy cache (HTTP proxy) - common files
ii squid-langpack 20220130-1 all Localized error pages for Squid
ii squidclient 5.7-2+deb12u1 amd64 Full featured Web Proxy cache (HTTP proxy) - HTTP(S) message utility
ii squidguard 1.6.0-4 amd64 filter and redirector plugin for Squid
ii sshguard 2.4.2-1+b2 amd64 Protects from brute force attacks against ssh
ii ssl-cert 1.1.2 all simple debconf wrapper for OpenSSL
ii sstp-client 1.0.18-1 amd64 Connect to a Microsoft Windows 2008 server using SSTP VPN
ii strongswan 5.9.11-2+vyos0 all IPsec VPN solution metapackage
ii strongswan-charon 5.9.11-2+vyos0 amd64 strongSwan Internet Key Exchange daemon
ii strongswan-libcharon 5.9.11-2+vyos0 amd64 strongSwan charon library
ii strongswan-starter 5.9.11-2+vyos0 amd64 strongSwan daemon starter and configuration file parser
ii strongswan-swanctl 5.9.11-2+vyos0 amd64 strongSwan IPsec client, swanctl command
ii stunnel4 3:5.68-2+deb12u1 amd64 Universal SSL tunnel for network daemons
ii sudo 1.9.13p3-1+deb12u1 amd64 Provide limited super user privileges to specific users
ii suricata 1:6.0.10-1 amd64 Next Generation Intrusion Detection and Prevention Tool
ii suricata-update 1.2.7-1 amd64 tool for updating Suricata rules
ii systemd 252.26-1~deb12u2 amd64 system and service manager
ii systemd-bootchart 234-2+b1 amd64 boot performance graphing tool
ii systemd-sysv 252.26-1~deb12u2 amd64 system and service manager - SysV compatibility symlinks
ii sysvinit-utils 3.06-4 amd64 System-V-like utilities
ii tar 1.34+dfsg-1.2+deb12u1 amd64 GNU version of the tar archiving utility
ii tcpdump 4.99.3-1 amd64 command-line network traffic analyzer
ii tcptraceroute 1.5beta7+debian-4.1+b1 amd64 traceroute implementation using TCP packets
ii telegraf 1.28.3-1 amd64 Plugin-driven server agent for reporting metrics into InfluxDB.
ii telnet 0.17+2.4-2+deb12u1 all transitional dummy package for inetutils-telnet default switch
ii tftpd-hpa 5.2+20150808-1.4 amd64 HPA's tftp server
ii tpm-udev 0.6 all udev rules for TPM modules
ii tpm2-tools 5.4-1 amd64 TPM 2.0 utilities
ii traceroute 1:2.1.2-1 amd64 Traces the route taken by packets over an IPv4/IPv6 network
ii tuned 2.20.0-1 all daemon for monitoring and adaptive tuning of system devices
ii twamp-client 4.4.6-1 amd64 TWAMP command line client utilities
ii twamp-server 4.4.6-1 amd64 TWAMP daemon
ii tzdata 2024a-0+deb12u1 all time zone and daylight-saving time data
ii ucf 3.0043+nmu1 all Update Configuration File(s): preserve user changes to config files
ii udev 252.26-1~deb12u2 amd64 /dev/ and hotplug management daemon
ii udp-broadcast-relay 0.1+vyos3+equuleus1 amd64 UDP Broadcast Packet Relay
ii uidmap 1:4.13+dfsg1-1+b1 amd64 programs to help use subuids
ii unionfs-fuse 1.0-1+b1 amd64 Fuse implementation of unionfs
ii usb-modeswitch 2.6.1-3+b1 amd64 mode switching tool for controlling "flip flop" USB devices
ii usb-modeswitch-data 20191128-5 all mode switching data for usb-modeswitch
ii usbutils 1:014-1+deb12u1 amd64 Linux USB utilities
ii usrmerge 37~deb12u1 all Convert the system to the merged /usr directories scheme
ii util-linux 2.38.1-5+deb12u1 amd64 miscellaneous system utilities
ii util-linux-extra 2.38.1-5+deb12u1 amd64 interactive login tools
ii uuid-runtime 2.38.1-5+deb12u1 amd64 runtime components for the Universally Unique ID library
ii virt-what 1.25-1 amd64 detect if we are running in a virtual machine
ii vyatta-bash 4.1-3+vyos2+current2 amd64 The VyOS Shell based on GNU bash
ii vyatta-biosdevname 1:0.3.11+vyos2+current2 amd64 VyOS version of the biosdevname utility.
ii vyatta-cfg 0.102.0+vyos2+current5 amd64 VyOS configuration system
ii vyatta-wanloadbalance 0.13.70+vyos2+current1 amd64 VyOS load balancing configuration system
ii vyos-1x 1.5dev0-1989-gad0acad65 amd64 VyOS configuration scripts and data
ii vyos-1x-vmware 1.5dev0-1989-gad0acad65 amd64 VyOS configuration scripts and data for VMware
ii vyos-http-api-tools 2.3 amd64 api tools for VyOS
ii vyos-intel-ixgbe 5.20.3 amd64 Vendor based driver for Intel ixgbe
ii vyos-intel-ixgbevf 4.18.9 amd64 Vendor based driver for Intel ixgbevf
ii vyos-intel-qat 4.24.0-00005-0 amd64 Vendor based driver for Intel QAT
ii vyos-linux-firmware 20240610 all Binary firmware for various drivers in the Linux kernel
ii vyos-user-utils 1.4.0+vyos1+current all VyOS user utilities metapackage
ii vyos-utils 0.0.3 amd64 VyOS utils for value validation and other things
ii vyos-xe-guest-utilities 7.13.0+vyos1.3 amd64 daemon for monitoring Xen Virtual machines
ii wget 1.21.3-1+b2 amd64 retrieves files from the web
ii whois 5.5.17 amd64 intelligent WHOIS client
ii wide-dhcpv6-client 20080615-23 amd64 DHCPv6 client for automatic IPv6 hosts configuration
ii wireguard-tools 1.0.20210914-1+b1 amd64 fast, modern, secure kernel VPN tunnel (userland utilities)
ii wireless-regdb 2022.06.06-1 all wireless regulatory database for Linux
ii wpasupplicant 2.10-2290-ge7172e26d amd64 client support for WPA and WPA2 (IEEE 802.11i)
ii xml-core 0.18+nmu1 all XML infrastructure and XML catalog file support
ii zabbix-agent2 1:6.0.14+dfsg-1+b1 amd64 Zabbix network monitoring solution - agent2
ii zlib1g:amd64 1:1.2.13.dfsg-1 amd64 compression library - runtime
ii zstd 1.5.4+dfsg2-5 amd64 fast lossless compression algorithm -- CLI tool

---

## Loaded Modules

8021q 36864 0 - Live 0x0000000000000000
garp 20480 1 8021q, Live 0x0000000000000000
mrp 20480 1 8021q, Live 0x0000000000000000
vxlan 86016 0 - Live 0x0000000000000000
ip6_udp_tunnel 16384 1 vxlan, Live 0x0000000000000000
udp_tunnel 20480 1 vxlan, Live 0x0000000000000000
ip_gre 28672 0 - Live 0x0000000000000000
gre 16384 1 ip_gre, Live 0x0000000000000000
ip6_tunnel 40960 0 - Live 0x0000000000000000
tunnel6 16384 1 ip6_tunnel, Live 0x0000000000000000
ipip 20480 0 - Live 0x0000000000000000
tunnel4 16384 1 ipip, Live 0x0000000000000000
ip_tunnel 32768 2 ip_gre,ipip, Live 0x0000000000000000
nft_ct 20480 12 - Live 0x0000000000000000
tls 114688 0 - Live 0x0000000000000000
nfnetlink_cthelper 20480 0 - Live 0x0000000000000000
xt_multiport 20480 0 - Live 0x0000000000000000
xt_mark 16384 0 - Live 0x0000000000000000
xt_comment 16384 1 - Live 0x0000000000000000
ip6table_filter 16384 0 - Live 0x0000000000000000
iptable_filter 16384 0 - Live 0x0000000000000000
ip6table_nat 16384 0 - Live 0x0000000000000000
iptable_nat 16384 0 - Live 0x0000000000000000
ip6_tables 32768 2 ip6table_filter,ip6table_nat, Live 0x0000000000000000
tap 28672 0 - Live 0x0000000000000000
tcp_bbr 20480 62 - Live 0x0000000000000000
xt_nat 16384 22 - Live 0x0000000000000000
xt_tcpudp 20480 22 - Live 0x0000000000000000
veth 32768 0 - Live 0x0000000000000000
xt_conntrack 16384 3 - Live 0x0000000000000000
nft_chain_nat 16384 19 - Live 0x0000000000000000
xt_MASQUERADE 20480 3 - Live 0x0000000000000000
nf_nat 49152 5 ip6table_nat,iptable_nat,xt_nat,nft_chain_nat,xt_MASQUERADE, Live 0x0000000000000000
nf_conntrack_netlink 49152 0 - Live 0x0000000000000000
nf_conntrack 172032 7 nft_ct,nfnetlink_cthelper,xt_nat,xt_conntrack,xt_MASQUERADE,nf_nat,nf_conntrack_netlink, Live 0x0000000000000000
nf_defrag_ipv6 24576 1 nf_conntrack, Live 0x0000000000000000
nf_defrag_ipv4 16384 1 nf_conntrack, Live 0x0000000000000000
xfrm_user 40960 1 - Live 0x0000000000000000
xfrm_algo 16384 1 xfrm_user, Live 0x0000000000000000
nft_counter 16384 132 - Live 0x0000000000000000
xt_addrtype 16384 4 - Live 0x0000000000000000
nft_compat 20480 55 - Live 0x0000000000000000
nf_tables 262144 345 nft_ct,nft_chain_nat,nft_counter,nft_compat, Live 0x0000000000000000
nfnetlink 20480 5 nfnetlink_cthelper,nf_conntrack_netlink,nft_compat,nf_tables, Live 0x0000000000000000
br_netfilter 32768 0 - Live 0x0000000000000000
bridge 307200 1 br_netfilter, Live 0x0000000000000000
stp 16384 2 garp,bridge, Live 0x0000000000000000
llc 16384 3 garp,bridge,stp, Live 0x0000000000000000
overlay 151552 5 - Live 0x0000000000000000
isofs 53248 1 - Live 0x0000000000000000
binfmt_misc 24576 1 - Live 0x0000000000000000
nls_iso8859_1 16384 1 - Live 0x0000000000000000
kvm_amd 155648 0 - Live 0x0000000000000000
ccp 106496 1 kvm_amd, Live 0x0000000000000000
kvm 1036288 1 kvm_amd, Live 0x0000000000000000
input_leds 16384 0 - Live 0x0000000000000000
serio_raw 20480 0 - Live 0x0000000000000000
virtio_input 20480 0 - Live 0x0000000000000000
sch_fq_codel 20480 3 - Live 0x0000000000000000
dm_multipath 40960 0 - Live 0x0000000000000000
scsi_dh_rdac 20480 0 - Live 0x0000000000000000
scsi_dh_emc 16384 0 - Live 0x0000000000000000
scsi_dh_alua 20480 0 - Live 0x0000000000000000
efi_pstore 16384 0 - Live 0x0000000000000000
ip_tables 32768 2 iptable_filter,iptable_nat, Live 0x0000000000000000
x_tables 53248 15 xt_multiport,xt_mark,xt_comment,ip6table_filter,iptable_filter,ip6table_nat,iptable_nat,ip6_tables,xt_nat,xt_tcpudp,xt_conntrack,xt_MASQUERADE,xt_addrtype,nft_compat,ip_tables, Live 0x0000000000000000
autofs4 49152 8 - Live 0x0000000000000000
btrfs 1564672 0 - Live 0x0000000000000000
blake2b_generic 20480 0 - Live 0x0000000000000000
zstd_compress 229376 1 btrfs, Live 0x0000000000000000
raid10 69632 0 - Live 0x0000000000000000
raid456 163840 0 - Live 0x0000000000000000
async_raid6_recov 24576 1 raid456, Live 0x0000000000000000
async_memcpy 20480 2 raid456,async_raid6_recov, Live 0x0000000000000000
async_pq 24576 2 raid456,async_raid6_recov, Live 0x0000000000000000
async_xor 20480 3 raid456,async_raid6_recov,async_pq, Live 0x0000000000000000
async_tx 20480 5 raid456,async_raid6_recov,async_memcpy,async_pq,async_xor, Live 0x0000000000000000
xor 24576 2 btrfs,async_xor, Live 0x0000000000000000
raid6_pq 122880 4 btrfs,raid456,async_raid6_recov,async_pq, Live 0x0000000000000000
libcrc32c 16384 5 nf_nat,nf_conntrack,nf_tables,btrfs,raid456, Live 0x0000000000000000
raid1 49152 0 - Live 0x0000000000000000
raid0 24576 0 - Live 0x0000000000000000
multipath 20480 0 - Live 0x0000000000000000
linear 20480 0 - Live 0x0000000000000000
virtio_gpu 73728 0 - Live 0x0000000000000000
virtio_dma_buf 16384 1 virtio_gpu, Live 0x0000000000000000
drm_kms_helper 311296 3 virtio_gpu, Live 0x0000000000000000
syscopyarea 16384 1 drm_kms_helper, Live 0x0000000000000000
sysfillrect 20480 1 drm_kms_helper, Live 0x0000000000000000
sysimgblt 16384 1 drm_kms_helper, Live 0x0000000000000000
fb_sys_fops 16384 1 drm_kms_helper, Live 0x0000000000000000
virtio_net 61440 0 - Live 0x0000000000000000
xhci_pci 24576 0 - Live 0x0000000000000000
cec 61440 1 drm_kms_helper, Live 0x0000000000000000
ahci 49152 0 - Live 0x0000000000000000
net_failover 20480 1 virtio_net, Live 0x0000000000000000
rc_core 65536 1 cec, Live 0x0000000000000000
psmouse 176128 0 - Live 0x0000000000000000
libahci 49152 1 ahci, Live 0x0000000000000000
drm 622592 3 virtio_gpu,drm_kms_helper, Live 0x0000000000000000
virtio_blk 20480 2 - Live 0x0000000000000000
virtio_rng 16384 0 - Live 0x0000000000000000
failover 16384 1 net_failover, Live 0x0000000000000000
xhci_pci_renesas 20480 1 xhci_pci, Live 0x0000000000000000
virtio_scsi 24576 1 - Live 0x0000000000000000

---

## CPU

---

## Installed CPU's

Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
Address sizes: 40 bits physical, 48 bits virtual
Byte Order: Little Endian
CPU(s): 4
On-line CPU(s) list: 0-3
Vendor ID: AuthenticAMD
Model name: QEMU Virtual CPU version 2.5+
CPU family: 15
Model: 107
Thread(s) per core: 1
Core(s) per socket: 4
Socket(s): 1
Stepping: 1
BogoMIPS: 1999.99
Flags: fpu de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx lm rep_good nopl cpuid extd_apicid pni cx16 hypervisor lahf_lm cmp_legacy svm 3dnowprefetch vmmcall
Virtualization: AMD-V
L1d cache: 256 KiB (4 instances)
L1i cache: 256 KiB (4 instances)
L2 cache: 2 MiB (4 instances)
L3 cache: 64 MiB (4 instances)
NUMA node(s): 1
NUMA node0 CPU(s): 0-3
Vulnerability Gather data sampling: Not affected
Vulnerability Itlb multihit: Not affected
Vulnerability L1tf: Not affected
Vulnerability Mds: Not affected
Vulnerability Meltdown: Not affected
Vulnerability Mmio stale data: Not affected
Vulnerability Reg file data sampling: Not affected
Vulnerability Retbleed: Not affected
Vulnerability Spec rstack overflow: Not affected
Vulnerability Spec store bypass: Not affected
Vulnerability Spectre v1: Mitigation; usercopy/swapgs barriers and \_\_user pointer sanitization
Vulnerability Spectre v2: Mitigation; Retpolines; STIBP disabled; RSB filling; PBRSB-eIBRS Not affected; BHI Not affected
Vulnerability Srbds: Not affected
Vulnerability Tsx async abort: Not affected

---

## Cumulative CPU Time Used by Running Processes

top - 16:02:54 up 7 days, 16:14, 2 users, load average: 0.66, 0.42, 0.37
Tasks: 47 total, 1 running, 46 sleeping, 0 stopped, 0 zombie
%Cpu(s): 0.0 us, 33.3 sy, 0.0 ni, 66.7 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
MiB Mem : 3907.0 total, 197.5 free, 1489.7 used, 2527.9 buff/cache
MiB Swap: 0.0 total, 0.0 free, 0.0 used. 2417.3 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND

13252 vyos 20 0 8640 4564 2668 R 12.5 0.1 0:00.03 top
1 root 20 0 103700 12980 8436 S 0.0 0.3 1:27.22 systemd
46 root 20 0 49500 16104 14872 S 0.0 0.4 0:02.56 systemd+
57 root 20 0 314724 71688 17240 S 0.0 1.8 0:42.77 python3
58 root 20 0 123168 30992 12124 S 0.0 0.8 0:02.78 python3
65 root 20 0 27792 9456 3784 S 0.0 0.2 0:28.33 systemd+
106 root 20 0 8408 4660 1468 S 0.0 0.1 0:02.00 haveged
272 root 20 0 4020 2396 2136 S 0.0 0.1 0:00.16 cron
275 message+ 20 0 8056 3096 2688 S 0.0 0.1 0:02.14 dbus-da+
363 root 20 0 25048 6756 5708 S 0.0 0.2 0:01.02 systemd+
366 daemon 20 0 3580 1128 988 S 0.0 0.0 0:00.01 atd
493 root 20 0 2480 1136 1020 S 0.0 0.0 0:14.28 netplugd
577 root 20 0 2936 948 864 S 0.0 0.0 0:00.01 agetty
828 root 15 -5 8856 3708 2232 S 0.0 0.1 0:31.29 watchfrr
847 frr 15 -5 1347676 11492 4456 S 0.0 0.3 0:03.07 zebra
852 frr 15 -5 10200 5308 2760 S 0.0 0.1 0:02.09 mgmtd
854 frr 15 -5 249812 14660 5812 S 0.0 0.4 0:09.23 bgpd
861 frr 15 -5 10684 5776 2896 S 0.0 0.1 0:01.97 ripd
864 frr 15 -5 10284 5472 2880 S 0.0 0.1 0:01.93 ripngd
867 frr 15 -5 13008 7428 3692 S 0.0 0.2 0:07.55 ospfd
870 frr 15 -5 11644 5888 2552 S 0.0 0.1 0:01.89 ospf6d
873 frr 15 -5 12796 6800 2864 S 0.0 0.2 0:01.90 isisd
877 frr 15 -5 10032 5040 2812 S 0.0 0.1 0:01.91 babeld
880 frr 15 -5 11632 5796 2736 S 0.0 0.1 0:02.38 pim6d
884 frr 15 -5 10280 7224 5424 S 0.0 0.2 0:00.09 ldpd
885 frr 15 -5 10280 7280 5480 S 0.0 0.2 0:00.08 ldpd
886 frr 15 -5 10932 5224 2680 S 0.0 0.1 0:02.00 ldpd
894 frr 15 -5 9988 4668 2460 S 0.0 0.1 0:01.92 staticd
897 frr 15 -5 10112 5216 2848 S 0.0 0.1 0:02.15 bfdd
1206 root 20 0 291432 3320 2804 S 0.0 0.1 0:00.33 rsyslogd
1316 \_chrony 20 0 18888 3160 2564 S 0.0 0.1 0:00.09 chronyd
1317 \_chrony 20 0 10560 2692 2128 S 0.0 0.1 0:00.07 chronyd
1519 root 20 0 15420 7660 6424 S 0.0 0.2 0:00.06 sshd
1578 root 0 -20 10740 9600 3764 S 0.0 0.2 0:00.96 atop
1597 root 20 0 2936 976 892 S 0.0 0.0 0:10.31 agetty
1605 root 20 0 17760 9064 7460 S 0.0 0.2 0:00.96 sshd
1608 vyos 20 0 19004 9132 7456 S 0.0 0.2 0:00.93 systemd
1609 vyos 20 0 104480 4648 0 S 0.0 0.1 0:00.00 (sd-pam)
1706 vyos 20 0 17760 6080 4208 S 0.0 0.2 0:02.50 sshd
1707 vyos 20 0 4996 4360 2668 S 0.0 0.1 0:00.91 vbash
1891 vyos 20 0 5744 5212 2760 S 0.0 0.1 1:09.85 vbash
4483 vyos 20 0 224600 292 0 S 0.0 0.0 0:00.39 unionfs+
8047 root 20 0 17764 10512 8904 S 0.0 0.3 0:00.97 sshd
8126 vyos 20 0 17764 6340 4464 S 0.0 0.2 0:00.24 sshd
8127 vyos 20 0 5112 4584 2772 S 0.0 0.1 0:00.80 vbash
8267 vyos 20 0 41004 34432 10052 S 0.0 0.9 0:32.21 python3
8268 vyos 20 0 2996 1192 1056 S 0.0 0.0 0:00.13 less

---

## Load Average

0.66 0.42 0.37 1/635 13253

---

## Hardware Interrupt Counters

CPU0 CPU1 CPU2 CPU3
0: 69 0 0 0 IO-APIC 2-edge timer
1: 0 0 0 9 IO-APIC 1-edge i8042
4: 802 1849 136 8 IO-APIC 4-edge ttyS0
8: 1 0 0 0 IO-APIC 8-edge rtc0
9: 0 0 0 0 IO-APIC 9-fasteoi acpi
12: 0 0 144 0 IO-APIC 12-edge i8042
24: 0 0 0 0 PCI-MSI 131072-edge virtio6-config
25: 0 0 0 9 PCI-MSI 131073-edge virtio6-virtqueues
26: 0 0 0 0 PCI-MSI 147456-edge virtio7-config
27: 0 3 0 0 PCI-MSI 147457-edge virtio7-virtqueues
28: 0 0 0 0 PCI-MSI 49152-edge virtio2-config
29: 0 0 0 10789 PCI-MSI 49153-edge virtio2-input
30: 0 0 0 0 PCI-MSI 163840-edge virtio8-config
31: 143903 0 0 0 PCI-MSI 163841-edge virtio8-req.0
32: 0 142352 0 0 PCI-MSI 163842-edge virtio8-req.1
33: 0 0 140278 0 PCI-MSI 163843-edge virtio8-req.2
34: 0 0 0 144173 PCI-MSI 163844-edge virtio8-req.3
35: 0 0 0 0 PCI-MSI 512000-edge ahci[0000:00:1f.2]
36: 0 0 0 0 PCI-MSI 32768-edge virtio1-config
37: 77317 164147 65078 178446 PCI-MSI 32769-edge virtio1-input.0
38: 63403 187771 68976 110750 PCI-MSI 32770-edge virtio1-output.0
39: 0 0 0 0 PCI-MSI 16384-edge virtio0-config
40: 0 0 0 0 PCI-MSI 16385-edge virtio0-control
41: 0 0 0 0 PCI-MSI 16386-edge virtio0-event
42: 0 0 0 0 PCI-MSI 114688-edge xhci_hcd
43: 89541 0 0 0 PCI-MSI 16387-edge virtio0-request
44: 0 77038 0 0 PCI-MSI 16388-edge virtio0-request
45: 0 0 59948 0 PCI-MSI 16389-edge virtio0-request
46: 0 0 0 106998 PCI-MSI 16390-edge virtio0-request
47: 0 0 0 0 PCI-MSI 114689-edge xhci_hcd
48: 0 0 0 0 PCI-MSI 114690-edge xhci_hcd
49: 0 0 0 0 PCI-MSI 114691-edge xhci_hcd
50: 0 0 0 0 PCI-MSI 114692-edge xhci_hcd
51: 0 0 0 0 PCI-MSI 65536-edge virtio3-config
52: 298216 808599 2005913 149010 PCI-MSI 65537-edge virtio3-control
53: 0 0 0 0 PCI-MSI 65538-edge virtio3-cursor
54: 0 0 0 0 PCI-MSI 81920-edge virtio4-config
55: 0 0 0 0 PCI-MSI 81921-edge virtio4-virtqueues
56: 0 0 0 0 PCI-MSI 98304-edge virtio5-config
57: 0 0 0 0 PCI-MSI 98305-edge virtio5-virtqueues
NMI: 0 0 0 0 Non-maskable interrupts
LOC: 83856436 83805947 83736804 85117063 Local timer interrupts
SPU: 0 0 0 0 Spurious interrupts
PMI: 0 0 0 0 Performance monitoring interrupts
IWI: 0 0 0 0 IRQ work interrupts
RTR: 0 0 0 0 APIC ICR read retries
RES: 3135442 3164523 3202400 3492383 Rescheduling interrupts
CAL: 29331601 28577598 27706176 26769219 Function call interrupts
TLB: 65205 58687 62325 60445 TLB shootdowns
TRM: 0 0 0 0 Thermal event interrupts
THR: 0 0 0 0 Threshold APIC interrupts
DFR: 0 0 0 0 Deferred Error APIC interrupts
MCE: 0 0 0 0 Machine check exceptions
MCP: 2131 2131 2131 2131 Machine check polls
ERR: 0
MIS: 0
PIN: 0 0 0 0 Posted-interrupt notification event
NPI: 0 0 0 0 Nested posted-interrupt event
PIW: 0 0 0 0 Posted-interrupt wakeup event

---

## Soft IRQ's

CPU0 CPU1 CPU2 CPU3
HI: 6 0 0 16
TIMER: 14942981 15407868 13011736 15365498
NET_TX: 93 108 126 123
NET_RX: 306076 505544 298724 450596
BLOCK: 112 289 156 327
IRQ_POLL: 0 0 0 0
TASKLET: 219 687 263 514
SCHED: 35999616 34265325 33590877 34469787
HRTIMER: 0 0 0 0
RCU: 35137660 34889630 34916699 35325884

---

## cat /proc/net/softnet_stat

0005320a 00000001 000000f4 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
00068f3b 00000005 000000e2 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000001
0004f641 00000004 000000bc 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000002
0006e5be 00000003 00000132 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000003

---

## Memory

---

## Installed Memory

MemTotal: 4000752 kB
MemFree: 202236 kB
MemAvailable: 2475312 kB
Buffers: 118640 kB
Cached: 2273064 kB
SwapCached: 0 kB
Active: 1212040 kB
Inactive: 2090000 kB
Active(anon): 3204 kB
Inactive(anon): 929464 kB
Active(file): 1208836 kB
Inactive(file): 1160536 kB
Unevictable: 53300 kB
Mlocked: 49300 kB
SwapTotal: 0 kB
SwapFree: 0 kB
Dirty: 1276 kB
Writeback: 0 kB
AnonPages: 963792 kB
Mapped: 440948 kB
Shmem: 9520 kB
KReclaimable: 196888 kB
Slab: 293892 kB
SReclaimable: 196888 kB
SUnreclaim: 97004 kB
KernelStack: 10208 kB
PageTables: 19360 kB
NFS_Unstable: 0 kB
Bounce: 0 kB
WritebackTmp: 0 kB
CommitLimit: 2000376 kB
Committed_AS: 3678088 kB
VmallocTotal: 34359738367 kB
VmallocUsed: 34024 kB
VmallocChunk: 0 kB
Percpu: 7520 kB
HardwareCorrupted: 0 kB
AnonHugePages: 0 kB
ShmemHugePages: 0 kB
ShmemPmdMapped: 0 kB
FileHugePages: 0 kB
FilePmdMapped: 0 kB
HugePages_Total: 0
HugePages_Free: 0
HugePages_Rsvd: 0
HugePages_Surp: 0
Hugepagesize: 2048 kB
Hugetlb: 0 kB
DirectMap4k: 255652 kB
DirectMap2M: 3934208 kB

---

## Memory Usage

total used free shared buff/cache available
Mem: 4000752 1525440 202236 9520 2588592 2475312
Swap: 0 0 0

---

## Devices

Character devices:
1 mem
4 /dev/vc/0
4 tty
4 ttyS
5 /dev/tty
5 /dev/console
5 /dev/ptmx
5 ttyprintk
7 vcs
10 misc
13 input
21 sg
29 fb
89 i2c
108 ppp
128 ptm
136 pts
180 usb
189 usb_device
204 ttyMAX
226 drm
229 hvc
237 aux
238 cec
239 lirc
240 vfio
241 virtio-portsdev
242 virtio-portsdev
243 bsg
244 watchdog
245 remoteproc
246 ptp
247 pps
248 rtc
249 dma_heap
250 dax
251 dimmctl
252 ndctl
253 tpm
254 gpiochip

Block devices:
7 loop
8 sd
9 md
11 sr
65 sd
66 sd
67 sd
68 sd
69 sd
70 sd
71 sd
128 sd
129 sd
130 sd
131 sd
132 sd
133 sd
134 sd
135 sd
252 virtblk
253 device-mapper
254 mdp
259 blkext

---

## Partitions

major minor #blocks name

7 0 65480 loop0
7 1 65480 loop1
7 2 89120 loop2
7 3 40036 loop3
7 4 89128 loop4
7 5 76056 loop5
7 6 39760 loop6
252 0 104857600 vda
252 1 104743919 vda1
252 14 4096 vda14
252 15 108544 vda15
11 0 271726 sr0
7 8 76056 loop8

---

## Partitioning for disk vda

Disk /dev/vda: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 \* 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 92CE6D7D-ACB9-4BD1-B74B-296DC5901CB3

Device Start End Sectors Size Type
/dev/vda1 227328 209715166 209487839 99.9G Linux filesystem
/dev/vda14 2048 10239 8192 4M BIOS boot
/dev/vda15 10240 227327 217088 106M EFI System

Partition table entries are not in disk order.

---

## Running Processes

UID PID PPID C STIME TTY TIME CMD
root 1 0 0 14:35 ? 00:00:37 /sbin/init
root 46 1 0 14:35 ? 00:00:02 /lib/systemd/systemd-journald
root 57 1 0 14:35 ? 00:00:14 /usr/bin/python3 -u /usr/libexec/vyos/services/vyos-configd
root 58 1 0 14:35 ? 00:00:02 /usr/bin/python3 -u /usr/libexec/vyos/services/vyos-hostsd
root 65 1 0 14:35 ? 00:00:05 /lib/systemd/systemd-udevd
root 106 1 0 14:35 ? 00:00:02 /usr/sbin/haveged --Foreground --verbose=1
root 272 1 0 14:36 ? 00:00:00 /usr/sbin/cron -f
message+ 275 1 0 14:36 ? 00:00:02 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
root 363 1 0 14:36 ? 00:00:01 /lib/systemd/systemd-logind
daemon 366 1 0 14:36 ? 00:00:00 /usr/sbin/atd -f
root 493 1 0 14:36 ? 00:00:00 /sbin/netplugd -p /var/run/netplugd.pid
root 577 1 0 14:36 pts/0 00:00:00 /sbin/agetty -o -p -- \u --noclear --keep-baud - 115200,38400,9600 xterm
root 828 1 0 14:36 ? 00:00:28 /usr/lib/frr/watchfrr -d -F traditional zebra mgmtd bgpd ripd ripngd ospfd ospf6d isisd babeld pim6d ldpd staticd bfdd
frr 847 1 0 14:36 ? 00:00:03 /usr/lib/frr/zebra -d -F traditional --daemon -A 127.0.0.1 -s 90000000
frr 852 1 0 14:36 ? 00:00:02 /usr/lib/frr/mgmtd -d -F traditional --daemon -A 127.0.0.1
frr 854 1 0 14:36 ? 00:00:09 /usr/lib/frr/bgpd -d -F traditional --daemon -A 127.0.0.1 -M rpki
frr 861 1 0 14:36 ? 00:00:01 /usr/lib/frr/ripd -d -F traditional --daemon -A 127.0.0.1
frr 864 1 0 14:36 ? 00:00:01 /usr/lib/frr/ripngd -d -F traditional --daemon -A ::1
frr 867 1 0 14:36 ? 00:00:07 /usr/lib/frr/ospfd -d -F traditional --daemon -A 127.0.0.1
frr 870 1 0 14:36 ? 00:00:01 /usr/lib/frr/ospf6d -d -F traditional --daemon -A ::1
frr 873 1 0 14:36 ? 00:00:01 /usr/lib/frr/isisd -d -F traditional --daemon -A 127.0.0.1
frr 877 1 0 14:36 ? 00:00:01 /usr/lib/frr/babeld -d -F traditional --daemon -A 127.0.0.1
frr 880 1 0 14:36 ? 00:00:02 /usr/lib/frr/pim6d -d -F traditional --daemon -A ::1
frr 884 1 0 14:36 ? 00:00:00 /usr/lib/frr/ldpd -L -u frr -g frr
frr 885 1 0 14:36 ? 00:00:00 /usr/lib/frr/ldpd -E -u frr -g frr
frr 886 1 0 14:36 ? 00:00:02 /usr/lib/frr/ldpd -d -F traditional --daemon -A 127.0.0.1
frr 894 1 0 14:36 ? 00:00:01 /usr/lib/frr/staticd -d -F traditional --daemon -A 127.0.0.1
frr 897 1 0 14:36 ? 00:00:02 /usr/lib/frr/bfdd -d -F traditional --daemon -A 127.0.0.1
root 1206 1 0 14:37 ? 00:00:00 /usr/sbin/rsyslogd -n -iNONE
\_chrony 1316 1 0 14:37 ? 00:00:00 /usr/sbin/chronyd -F 1 -f /run/chrony/chrony.conf
\_chrony 1317 1316 0 14:37 ? 00:00:00 /usr/sbin/chronyd -F 1 -f /run/chrony/chrony.conf
root 1519 1 0 14:37 ? 00:00:00 sshd: /usr/sbin/sshd -f /run/sshd/sshd_config [listener] 0 of 10-100 startups
root 1578 1 0 14:37 ? 00:00:00 /usr/bin/atop -w /var/log/atop/atop.log 600
root 1597 1 0 14:37 ? 00:00:10 /sbin/agetty -o -p -- \u --keep-baud 115200 ttyS0 vt220
root 1605 1519 0 14:38 ? 00:00:00 sshd: vyos [priv]
vyos 1608 1 0 14:38 ? 00:00:00 /lib/systemd/systemd --user
vyos 1609 1608 0 14:38 ? 00:00:00 (sd-pam)
vyos 1706 1605 0 14:38 ? 00:00:02 sshd: vyos@pts/1
vyos 1707 1706 0 14:38 pts/1 00:00:00 -vbash
vyos 1891 1707 0 14:59 pts/1 00:00:04 vbash
vyos 4483 1 0 15:33 ? 00:00:00 unionfs-fuse -o cow -o allow_other /opt/vyatta/config/tmp/changes_only_1891=RW:/opt/vyatta/config/active=RO /opt/vyatta/config/tmp/new_config_1891
root 8047 1519 0 16:02 ? 00:00:00 sshd: vyos [priv]
vyos 8126 8047 0 16:02 ? 00:00:00 sshd: vyos@pts/2
vyos 8127 8126 0 16:02 pts/2 00:00:00 -vbash
vyos 8267 8127 2 16:02 pts/2 00:00:00 python3 /usr/libexec/vyos/op_mode/show_techsupport_report.py
vyos 8268 8127 0 16:02 pts/2 00:00:00 less --buffers=64 --auto-buffers --no-lessopen --QUIT-AT-EOF --quit-if-one-screen --RAW-CONTROL-CHARS --squeeze-blank-lines --no-init
vyos 13263 8267 0 16:02 pts/2 00:00:00 ps -ef
`````

</details>

## 参考

- [Vyatta(VyOS) EVPN 設定 | ネットワークチェンジニアとして](https://changineer.info/network/vyatta/vyatta_tunnel_evpn.html)
