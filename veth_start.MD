# Compile the p4 program in intel vm

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
3. ``` ./run_tofino_model.sh -p simple_l3 ``` 

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

5. 
6.  asdf 
7.  
