# int_experiment

cpu_port example : 
```
nagumahu1@ubuntunagumahu1:~/mysde$ sudo tshark -i enp4s0f1 
Running as user "root" and group "root". This could be dangerous.
tshark: Lua: Error during loading:
 [string "/usr/share/wireshark/init.lua"]:44: dofile has been disabled due to running Wireshark as superuser. See https://wiki.wireshark.org/CaptureSetup/CapturePrivileges for help in running Wireshark as an unprivileged user.
Capturing on 'enp4s0f1'
    1 0.000000000 aa:aa:aa:aa:aa:aa → 00:cc:00:01:02:03 0xc002 281 Ethernet II
    2 30.002933848 aa:aa:aa:aa:aa:aa → 00:cc:00:01:02:03 0xc002 281 Ethernet II
```
