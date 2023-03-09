# check if the port is open 

```
grep -w 80 /etc/services
```

port 80 is open.


```
grep -w 5001 /etc/services
```

The port was not open. Open the port on both hosts: 
```
sudo ufw allow 5001/tcp
```
