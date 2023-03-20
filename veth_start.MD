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
4. asd 
5. 
6.  asdf 
7.  
