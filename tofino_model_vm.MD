# ICA 1131 Lab Guid 

To build tofino model SDE on a virtual machine : 

1. Create a fresh VM with Ubuntu Linux(either 16.04 or 18.04) right on your PC or MAC. 
2. Create VM based on it, copy the SDE tarball in there and do the build. 
3. ```tar xzvf ~/Downloads/bf-sde-x.y.z.tgz```
4. ```cd bf-sde-x.y.z.tgz```
5. ```./p4studio interactive``` 
```
Do you want to install dependencies? [Y/n]: Y
Do you want to build switch-p4-16? [y/N]: Y
Please provide the profile to build switch with (x1_tofino, x2_tofino, g1_tofino, y1_tofino2, y2_tofino2, y3_tofino2, z2_tofino2) [x1_tofino]: x1_tofino
Do you want to build bf-diags? [y/N]: N
Do you want to build P4-14 examples? [y/N]: N
Do you want to build P4-16 examples? [Y/n]: Y
Please provide architecture for bf-diags and p4-examples (tofino, tofino2, tofino2m, tofino2h, all) [tofino]: tofino
Do you want to build for HW? [y/N]: N
Do you want to enable P4Runtime? [y/N]: N

Created profile:
global-options: {}
features:
  p4-examples:
  - p4-16-programs
  switch:
    profile: x1_tofino
architectures:
- tofino

Do you want to write it to a file? [y/N]: Y
Please provide the profile filename - [Example:profiles/my-profile.yaml]: ./profiles/vm_model.yaml
Do you want to continue building SDE? [y/N]: N
```
6.  ```./p4studio profile describe ./profiles/vm_model.yaml```

```
Loading profile from ./profiles/vm_model.yaml file...
Profile is correct.

Source packages to install: 
 - bridge
 - libcli
 - thrift
 - grpc
Configuration options: 
 ✓ switch
 ✓ tofino
 ✗ tofino2
 ✗ tofino2m
 ✗ tofino2h
Targets to build: 
 - p4-16-programs
 - x1_tofino

Profile is equivalent to below list of commands:
p4studio dependencies install --source-packages bridge,libcli,thrift,grpc --jobs N
p4studio configure tofino switch '^tofino2m' '^tofino2' '^tofino2h'
p4studio build --jobs N p4-16-programs x1_tofino
```
7.  ```vim ./profiles/vm_model.yaml ``` Add tofino2 to the file. 
```
global-options: {}
features:
  p4-examples:
  - p4-16-programs
  switch:
    profile: x1_tofino
architectures:
- tofino
- tofino2
```

# Build the SDE 

8.  Now, we can build the SDE using: ``` ./p4studio profile apply ./profiles/vm_model.yaml ``` 
9.  We can check logs in ``` ./mysde/p4studio/logs``` folder. 
10.  ```./run_tofino_model.sh -p diag --int-port-loop 5 ``` 
11. ```./run_switchd.sh -p diag```

```
bfshell> ucliStarting UCLI from bf-shell 

Cannot read termcap database;
using dumb terminal settings.
bf-sde> diags help
  lpbk-setup      lpbk-setup <dev> <port-range> <loop-mode: 0=none,1=mac,2=phy,3=ext,4=pcs,5=pipe>
  lpbk-start      lpbk-start <sess-hdl(0=default)> <num-pkt> <pkt-size>
  lpbk-stop       lpbk-stop <sess-hdl(0=default)>
  lpbk-status     lpbk-status <sess-hdl(0=default)>
  lpbk-cleanup    lpbk-cleanup <sess-hdl(0=default)>
  snake-setup     snake-setup <dev> <port-range> <loop-mode: 0=none,1=mac,2=phy,3=ext,4=pcs,5=pipe>
  snake-start     snake-start <sess-hdl(0=default)> <num-pkt> <pkt-size> <bidir-traffic>(0:non-bidir, 1:bidir)
  snake-stop      snake-stop<sess-hdl(0=default)>
  snake-status    snake-status <sess-hdl(0=default)>
  snake-cleanup   snake-cleanup <sess-hdl(0=default)>
  pair-setup      pair-setup <dev> <port-range> <loop-mode: 0=none,1=mac,2=phy,3=ext,4=pcs,5=pipe>
  pair-start      pair-start <sess-hdl(0=default)> <num-pkt> <pkt-size> <bidir-traffic(0:non-bidir, 1:bidir)>
  pair-stop       pair-stop <sess-hdl(0=default)>
  pair-status     pair-status <sess-hdl(0=default)> [<detail(0=ON,1=OFF)>]
  pair-cleanup    pair-cleanup <sess-hdl(0=default)>
  mlpbk-setup     mlpbk-setup <dev> <ports> <loop-mode: 0=none,1=mac,2=phy,3=ext,4=pcs,5=pipe>
  mlpbk-start     mlpbk-start <sess-hdl(0=default)> <num-pkt> <pkt-size>
  mlpbk-stop      mlpbk-stop <sess-hdl(0=default)>
  mlpbk-status    mlpbk-status <sess-hdl(0=default)>
  mlpbk-cleanup   mlpbk-cleanup <sess-hdl(0=default)>
  sess-valid      sess-valid <sess-hdl>
  sess-del-all    sess-del-all <dev>
  sess-print      sess-print <sess-hdl (0=all)>
  lpbk-mode-set   lpbk-mode-set <dev> <dev-port> <loop-mode: 0=none,1=mac,2=phy,3=ext,4=pcs,5=pipe>
  fwd-rule-add    fwd-rule-add <dev> <ig-port> <eg-port> <tcpDstPort-start> <tcpDstPort-end> <priority>
  fwd-rule-del    fwd-rule-del <dev> <entry-hdl>
  cpu-port-print  cpu-port-print <dev>
  cpu-stats-show  cpu-stats-show <dev> <type: 0=one port,1=all ports> <dev_port>
  cpu-stats-clear cpu-stats-clear <dev> <type: 0=one port,1=all ports> <dev_port>
  pkt-inj         pkt-inj <dev> <port-range> <num-pkt> <pkt-size>
  vlan-create     vlan-create <dev> <vlan-id>
  port-vlan-add   port-vlan-add <dev> <port-range> <vlan-id>
  port-vlan-del   port-vlan-del <dev> <port-range> <vlan-id>
  def-vlan-set    def-vlan-set <dev> <port> <vlan-id>
  def-vlan-reset  def-vlan-reset <dev> <port>
  vlan-destroy    vlan-destroy <dev> <vlan-id>
  vlan-show       vlan-show <dev> <vlan-id>
  vlan-show-all   vlan-show-all <dev>
  pkt-logs        pkt-logs <level: 0=off,1=err,2:all>
  data-pattern    data-pattern <sess-hdl> <mode: 0=random,1=fixed> <start-pattern> <start-pattern-len> <pattern_a> <pattern_b> <each-pattern-len>
  pkt-payload     pkt-payload <sess-hdl> <mode: 0=random,1=fixed,2=random-flip> <"payload" (""=None)> <"payload-file-path" (""=None)>
  pkt-contents    pkt-contents <sess-hdl> <mode: 0=random,1=fixed>
  lrn-timeout     lrn-timeout <dev> <usec>
  mac-aging       mac-aging <dev> <msec>
  pktid-cnt-show  pktid-cnt-show <dev>
  pktid-cnt-clear pktid-cnt-clear <dev>
  drain-all-pkts  drain-all-pkts <dev> <mode: 0=off,1=on>
  sess-max        sess-max <dev> <max-value(default=32)>
  pkt-rx-process  pkt-rx-process <dev> <mode: 0=disable,1=enable>
  profile-show    profile-show
  log 
```

12.  ```ucli ```
``` bfshell> ucliStarting UCLI from bf-shell 

Cannot read termcap database;
using dumb terminal settings.
bf-sde>  
```

13.  ```diags snake-setup 0 0,1,256,257 3```

```Allocated handle 2 on dev 0
dst-override-add: ig_port 320, dst-port 0, tcp (1024-2047), pri 0 
diag:: Snake test setup <dev=0> <port-range=0,1,256,257><loop-mode=3> 
Num ports is 4 
Ports -> 0,1,256,257
dst-override-add: ig_port 0, dst-port 257, tcp (33792-34815), pri 500 
dst-override-add: ig_port 0, dst-port 1, tcp (1024-2047), pri 500 
dst-override-add: ig_port 1, dst-port 0, tcp (33792-34815), pri 500 
dst-override-add: ig_port 1, dst-port 256, tcp (1024-2047), pri 500 
dst-override-add: ig_port 256, dst-port 1, tcp (33792-34815), pri 500 
dst-override-add: ig_port 256, dst-port 257, tcp (1024-2047), pri 500 
dst-override-add: ig_port 257, dst-port 256, tcp (33792-34815), pri 500 
dst-override-add: ig_port 320, dst-port 257, tcp (33792-34815), pri 0 
dst-override-add: ig_port 257, dst-port 0, tcp (1024-2047), pri 500 
Snake test setup success 
Snake Session Handle: 2 
```
14. ```diags snake-start 1 1 200 1``` 

``` Pkt Tx API invoked for dev 0 
diag:: Snake test start <ses========= Successfully sent pkt with id 1000000000000 from CPU to port 0 of size 200 in session 1 tcp-dst-port 0 pkt-num 1 =========
s-hdl=1> <num-pkt========== Successfully sent pkt with id 1010100000001 from CPU to port 257 of size 200 in session 1 tcp-dst-port 32768 pkt-num 1 =========
1> <pkt-size=200> <bidir=1>
Snake test started 
```
15. ``` diags snake-stop 1 ```  
```
Snake Stop for tcp range (0 - 350) 
didst-override-add: ig_port 257, dst-port 320, tcp (0-350), pri 0 
ag:: Snake Test stop <sess-hdl=1>
========= Start processing for pkt_id 1000000000000 from port 257 of size 200 in session 1 =========
  Valid diag pkt with id 1000000000000 on from port 257 of size 200 in session 1
========= End Processing for pkt_id   1000000000000 from port 257 of size 200 in session 1 ========= 
Snake Stop for tcp range (0 - 700) 
dst-override-del: handle 22 
dst-override-add: ig_port 257, dst-port 320, tcp (0-700), pri 0 
Snake Stop for tcp range (0 - 1023) 
dst-override-del: handle 22 
dst-override-add: ig_port 257, dst-port 320, tcp (0-1023), pri 0 
dst-override-del: handle 22 
Snake Stop for tcp range (32768 - 33118) 
dst-override-add: ig_port 0, dst-port 320, tcp (32768-33118), pri 0 
========= Start processing for pkt_id 1010100000001 from port 0 of size 200 in session 1 =========
  Valid diag pkt with id 1010100000001 on from port 0 of size 200 in session 1
========= End Processing for pkt_id   1010100000001 from port 0 of size 200 in session 1 ========= 
Snake Stop for tcp range (32768 - 33468) 
dst-override-del: handle 22 
dst-override-add: ig_port 0, dst-port 320, tcp (32768-33468), pri 0 
Snake Stop for tcp range (32768 - 33791) 
dst-override-del: handle 22 
dst-override-add: ig_port 0, dst-port 320, tcp (32768-33791), pri 0 
dst-override-del: handle 22 
Snake Stop DONE 
Test stop success 
```

16. ``` diags snake-status 1 ```

```
diag:: Snake Test status <sess-hdl=1>
  Test Status: Pass 
Stats: Tx-total=2, rx-total=2, rx-good=2, rx_bad=0 
No of Tx packet completions: 2
```

#Question: Why do you think "No of Tx packet completions: 2" ? 

# Checking the port counters. 

17. ```pm```
```bf-sde.pm>   ``` 
18. ```show -p 1/-```
```
-----+----+---+----+-------+----+--+--+---+---+---+--------+----------------+----------------+-
PORT |MAC |D_P|P/PT|SPEED  |FEC |AN|KR|RDY|ADM|OPR|LPBK    |FRAMES RX       |FRAMES TX       |E
-----+----+---+----+-------+----+--+--+---+---+---+--------+----------------+----------------+-
1/0  |15/0|  0|0/ 0|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |            2752|            2752| 
1/1  |15/1|  1|0/ 1|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |            2752|            2752| 
1/2  |15/2|  2|0/ 2|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |               0|               0| 
1/3  |15/3|  3|0/ 3|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |               0|               0| 
```

19. ``` show -p 33/-```
```
-----+----+---+----+-------+----+--+--+---+---+---+--------+----------------+----------------+-
PORT |MAC |D_P|P/PT|SPEED  |FEC |AN|KR|RDY|ADM|OPR|LPBK    |FRAMES RX       |FRAMES TX       |E
-----+----+---+----+-------+----+--+--+---+---+---+--------+----------------+----------------+-
33/0 |47/0|256|2/ 0|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |            2752|            2752| 
33/1 |47/1|257|2/ 1|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |            2752|            2752| 
33/2 |47/2|258|2/ 2|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |               0|               0| 
33/3 |47/3|259|2/ 3|10G    |NONE|Au|Au|YES|DIS|DWN|  NONE  |               0|               0| 
```

We can also retriev more detailed SNMP counters using : 

20. ``` show -d -p 1/-```
```
================================================================================
             1/0 : Port Identifier
              NO : is port internal
            15/0 : MAC
               0 : Dev Port
            0/ 0 : Pipe/Port 
         10G     : Speed
            NONE : FEC
             YES : Ready for Bring Up
              NO : Autoneg eligibility
         DEFAULT : AN policy set
             DIS : Admin State
            DOWN : Operational Status
            2752 : FramesReceivedOK
            2752 : FramesReceivedAll
               0 : FramesReceivedwithFCSError
               0 : FrameswithanyError
          550400 : OctetsReceivedinGoodFrames
          550400 : OctetsReceived
               0 : FramesReceivedwithUnicastAddresses
            2752 : FramesReceivedwithMulticastAddresses
               0 : FramesReceivedwithBroadcastAddresses
               ...
```
21. 
```
bf-sde.pm> 
bf-sde.pm> ..
bf-sde>
```


# Cleaning up 

22. ```diags snake-cleanup 1 ```
```
dst-override-del: handle 4 
diag:: Snake Test cleanup <sess-hdl=1>
dst-override-del: handle 3 
dst-override-del: handle 2 
dst-override-del: handle 6 
dst-override-del: handle 5 
dst-override-del: handle 8 
dst-override-del: handle 7 
dst-override-del: handle 11 
dst-override-del: handle 9 
dst-override-del: handle 10 
Cleaning up pkt database for session 1
Freed handle 1 on dev 0
Test cleanup success 
``` 
