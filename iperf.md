# check if the port is open 

```
grep -w 80 /etc/services
```

port 80 is open.


```
grep -w 5001 /etc/services
```

Port 5001 is closed. 
The port was not open. Open the port on both hosts: 

# Open the ports in linux ubuntu : 

```
sudo ufw allow 5001/tcp
```

On server side : ``` iperf3 -s ``` We are getting : 
```
-----------------------------------------------------------
Server listening on 5201 (test #1)
-----------------------------------------------------------
```

On client side : ```  iperf3 -c 134.197.113.78 ```
```
Connecting to host 134.197.113.78, port 5201
[  5] local 134.197.113.68 port 42544 connected to 134.197.113.78 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  37.8 MBytes   317 Mbits/sec  1326   1.45 MBytes       
[  5]   1.00-2.00   sec  12.5 MBytes   105 Mbits/sec  2207   1.72 MBytes       
[  5]   2.00-3.00   sec  12.5 MBytes   105 Mbits/sec  2978   1.91 MBytes       
[  5]   3.00-4.00   sec  13.8 MBytes   115 Mbits/sec  3995   2.17 MBytes       
[  5]   4.00-5.00   sec  13.8 MBytes   115 Mbits/sec  4230   2.36 MBytes       
[  5]   5.00-6.00   sec  15.0 MBytes   126 Mbits/sec  5243   2.59 MBytes       
[  5]   6.00-7.00   sec  15.0 MBytes   126 Mbits/sec  6477   2.81 MBytes       
[  5]   7.00-8.00   sec  17.5 MBytes   147 Mbits/sec  6973   3.02 MBytes       
[  5]   8.00-9.00   sec  16.2 MBytes   136 Mbits/sec  7100   3.25 MBytes       
[  5]   9.00-10.00  sec  18.8 MBytes   157 Mbits/sec  9219   3.46 MBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   173 MBytes   145 Mbits/sec  49748             sender
[  5]   0.00-10.00  sec   164 MBytes   138 Mbits/sec                  receiver

iperf Done.
```

# Conclusion 

If ```ARP``` protocol is not implemented than ```iperf``` and ```ping``` will not work. 
