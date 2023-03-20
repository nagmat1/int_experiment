# Compile the p4 program in intel vm ICA 1111

1. ``` ./tools/p4_build.sh -p  ~/tof_model/exercises/01_simple_l3/simple_l3.p4 ```
```
Using SDE          /home/nnazarov/tof_model/mysde
Using SDE_INSTALL /home/nnazarov/tof_model/mysde/install
Using SDE version bf-sde-9.7.0

OS Name: Ubuntu 18.04.6 LTS
This system has 131GB of RAM and 32 CPU(s)
Parallelization:  Recommended: -j32   Actual: -j32

Compiling for p4_16/tna
P4 compiler path:    /home/nnazarov/tof_model/mysde/install/bin/bf-p4c
P4 compiler version: 9.7.0 (SHA: da5115f) (p4c-based)
Build Dir: /home/nnazarov/tof_model/mysde/build/p4-build/tofino/simple_l3
 Logs Dir: /home/nnazarov/tof_model/mysde/logs/p4-build/tofino/simple_l3

  Building simple_l3        CLEAR CMAKE MAKE INSTALL ... DONE
```

# Virtual ethernets neet to be executed after each reboot. 

2. ```sudo $SDE_INSTALL_bin_veth_setup.sh``` 
```
No of Veths is 64
Adding CPU veth
```
3. Run Tofino model on Virtual Machine : 
``` ./run_tofino_model.sh -p simple_l3 ``` 

```
Using SDE /home/nnazarov/tof_model/mysde
Using SDE_INSTALL /home/nnazarov/tof_model/mysde/install
Model using test directory: 
Model using port info file: None
Using PATH /home/nnazarov/tof_model/mysde/install/bin:/home/nnazarov/tof_model/mysde/install/bin:/home/nnazarov/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
Using LD_LIBRARY_PATH /usr/local/lib:/home/nnazarov/tof_model/mysde/install/lib:
 PRIVS: Eff=0x00000000 Perm=0x00002006 Inh=0x00000000
Performing preliminary checks on config file
Opening p4 target config file '/home/nnazarov/tof_model/mysde/install/share/p4/targets/tofino/simple_l3.conf' ...
Loaded p4 target config file
 Package size 1
 No of Chips is 1
Chip part revision number is 1
 No of Packages is 1
Chip 0 SKU: defaulting to BFN77110
Chip 0 SKU setting: sku 0 pipe mode 0
Chip 0 Physical pipes enabled bitmap 0xf 
Adding interface veth0 as port 0
Adding interface veth2 as port 1
Adding interface veth4 as port 2
Adding interface veth6 as port 3
Adding interface veth8 as port 4
Adding interface veth10 as port 5
Adding interface veth12 as port 6
Adding interface veth14 as port 7
Adding interface veth16 as port 8
Adding interface veth18 as port 9
Adding interface veth20 as port 10
Adding interface veth22 as port 11
Adding interface veth24 as port 12
Adding interface veth26 as port 13
Adding interface veth28 as port 14
Adding interface veth30 as port 15
Adding interface veth32 as port 16
Adding interface veth250 as port 64
Simulation target: Asic Model
Using TCP port range: 8001-8004
Listen socket created
bind done on port 8001. Listening..
Waiting for incoming connections...
CLI listening on port 8000
```

4.Load the P4 program onto the switch : 
```./run_switchd.sh -p simple_l3``` 

```
Using SDE /home/nnazarov/tof_model/mysde
Using SDE_INSTALL /home/nnazarov/tof_model/mysde/install
Setting up DMA Memory Pool
[sudo] password for nnazarov: 
Using TARGET_CONFIG_FILE /home/nnazarov/tof_model/mysde/install/share/p4/targets/tofino/simple_l3.conf
Using PATH /home/nnazarov/tof_model/mysde/install/bin:/home/nnazarov/tof_model/mysde/install/bin:/home/nnazarov/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
Using LD_LIBRARY_PATH /usr/local/lib:/home/nnazarov/tof_model/mysde/install/lib:
bf_sysfs_fname /sys/class/bf/bf0/device/dev_add
Install dir: /home/nnazarov/tof_model/mysde/install (0x557938898810)
bf_switchd: system services initialized
bf_switchd: loading conf_file /home/nnazarov/tof_model/mysde/install/share/p4/targets/tofino/simple_l3.conf...
bf_switchd: processing device configuration...
Configuration for dev_id 0
  Family        : tofino
  pci_sysfs_str : /sys/devices/pci0000:00/0000:00:03.0/0000:05:00.0
  pci_domain    : 0
  pci_bus       : 5
  pci_fn        : 0
  pci_dev       : 0
  pci_int_mode  : 1
  sbus_master_fw: /home/nnazarov/tof_model/mysde/install/
  pcie_fw       : /home/nnazarov/tof_model/mysde/install/
  serdes_fw     : /home/nnazarov/tof_model/mysde/install/
  sds_fw_path   : /home/nnazarov/tof_model/mysde/install/share/tofino_sds_fw/avago/firmware
  microp_fw_path: 
bf_switchd: processing P4 configuration...
P4 profile for dev_id 0
num P4 programs 1
  p4_name: simple_l3
  p4_pipeline_name: pipe
    libpd: 
    libpdthrift: 
    context: /home/nnazarov/tof_model/mysde/install/share/tofinopd/simple_l3/pipe/context.json
    config: /home/nnazarov/tof_model/mysde/install/share/tofinopd/simple_l3/pipe/tofino.bin
  Pipes in scope [0 1 2 3 ]
  diag: 
  accton diag: 
  Agent[0]: /home/nnazarov/tof_model/mysde/install/lib/libpltfm_mgr.so
  non_default_port_ppgs: 0
 ... 
 
```
5. Load the bfrt python scripts to the p4 program : 
```./run_bfshell.sh -b ~/tof_model/exercises/01_simple_l3/setup.py ```
```
Using SDE /home/nnazarov/tof_model/mysde
Using SDE_INSTALL /home/nnazarov/tof_model/mysde/install
Connecting to localhost port 7777 to check status on these devices: [0]
Waiting for device 0 to be ready
/home/nnazarov/tof_model/mysde/install/bin/bfshell /home/nnazarov/tof_model/exercises/01_simple_l3/setup.py
bfrt_python /home/nnazarov/tof_model/exercises/01_simple_l3/setup.py
exit

        ********************************************
        *      WARNING: Authorised Access Only     *
        ********************************************
    

bfshell> bfrt_python /home/nnazarov/tof_model/exercises/01_simple_l3/setup.py
cwd : /home/nnazarov/tof_model/mysde

Devices found :  [0]
We've found 1 p4 programs for device 0:
simple_l3
Creating tree for dev 0 and program simple_l3

/home/nnazarov/tof_model/mysde/install/lib/python3.8/site-packages/IPython/core/history.py:226: UserWarning: IPython History requires SQLite, your history will not be saved
  warn("IPython History requires SQLite, your history will not be saved")
Python 3.8.10 (default, Mar 15 2023, 16:30:07) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.18.1 -- An enhanced Interactive Python. Type '?' for help.

******************* PROGAMMING RESULTS *****************

Table ipv4_host:
----- ipv4_host Dump Start -----
Default Entry:
Entry data (action : NoAction):

pipe.Ingress.ipv4_host entries for action: Ingress.send
hdr.ipv4.dst_addr    port
-------------------  ------
0xC0A80101           0x01
0xC0A80102           0x02
0xC0A801FE           0x40


pipe.Ingress.ipv4_host entries for action: Ingress.drop
hdr.ipv4.dst_addr
-------------------
0xC0A80103

----- ipv4_host Dump End -----
Table ipv4_lpm:
----- ipv4_lpm Dump Start -----
Default Entry:
Entry data (action : Ingress.send):
    port                           : 0x40

pipe.Ingress.ipv4_lpm entries for action: Ingress.send
hdr.ipv4.dst_addr             port
----------------------------  ------
('0xC0A80100', '0x00000018')  0x01
('0x00000000', '0x00000000')  0x40


pipe.Ingress.ipv4_lpm entries for action: Ingress.drop
hdr.ipv4.dst_addr
----------------------------
('0xC0A80000', '0x00000010')


----- ipv4_lpm Dump End -----
bfshell> exit
```

```./run_bfshell.sh -b ~/tof_model/exercises/01_simple_l3/setup.py -i``` #-i flag :Execute a prepared python script and continue interactively. 

6.  
