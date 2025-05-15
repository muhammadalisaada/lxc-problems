# lxc-problems
LXC containers on ubuntu without ip4

I have server ubuntu 22.04 and when I running lxc container it still without ip address and I can't connect to it or ping

```
blabla@blabla:~$ lxc list
+---------+---------+------+-----------------------------------------------+-----------+-----------+
|  NAME   |  STATE  | IPV4 |                     IPV6                      |   TYPE    | SNAPSHOTS |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
| mariadb | RUNNING |      | fd42:594a:5292:77f3:216:3eff:fe3c:7abe (eth0) | CONTAINER | 0         |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
| nginx1  | RUNNING |      | fd42:594a:5292:77f3:216:3eff:fe85:b910 (eth0) | CONTAINER | 0         |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
| nginx2  | RUNNING |      | fd42:594a:5292:77f3:216:3eff:feb3:3103 (eth0) | CONTAINER | 0         |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
| nginx3  | RUNNING |      | fd42:594a:5292:77f3:216:3eff:feaf:5288 (eth0) | CONTAINER | 0         |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
| proxy   | RUNNING |      | fd42:594a:5292:77f3:216:3eff:fee7:5013 (eth0) | CONTAINER | 0         |
+---------+---------+------+-----------------------------------------------+-----------+-----------+
blabla@blabla:~$ lxc network list
+--------+----------+---------+----------------+---------------------------+-------------+---------+
|  NAME  |   TYPE   | MANAGED |      IPV4      |           IPV6            | DESCRIPTION | USED BY |
+--------+----------+---------+----------------+---------------------------+-------------+---------+
| eth0   | physical | NO      |                |                           |             | 0       |
+--------+----------+---------+----------------+---------------------------+-------------+---------+
| lxdbr0 | bridge   | YES     | 10.88.102.1/24 | fd42:594a:5292:77f3::1/64 |             | 6       |
+--------+----------+---------+----------------+---------------------------+-------------+---------+
```



this worked for me: 
sudo ufw allow in on lxdbr0
sudo ufw route allow in on lxdbr0
sudo ufw route allow out on lxdbr0

you need to allow traffic to your container

https://documentation.ubuntu.com/lxd/latest/howto/network_bridge_firewalld/#ufw-add-rules-for-the-bridge

https://discuss.linuxcontainers.org/t/lxd-bridge-doesnt-work-with-ipv4-and-ufw-with-nftables/10034/17?u=juanmitaboada

http://serverfault.com/questions/1089692/lxc-instances-do-not-have-ipv4-addresses
