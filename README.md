# Network-Display
Some scripts that make network display more intuitive on Linux
# 使用案例
## routel
Linux下存在iproute2包可以配置内核的ip，路由，接口等信息，其中，`ip route route show table all`命令可以看到所有路由表内的路由，但显示出的效果非常杂乱。  

默认情况下，存在一个`/usr/bin/routel`程序，使用`routel`命令可以有类似网络路由器那样的路由表显示，但还是存在部分缺陷。  

因此我更改了routel程序内容，增加了颜色分类和Metric显示，使用时直接把我存储库中的routel内容覆盖掉你`/usr/bin/routel`内容即可。效果如下：  

<img width="1453" height="742" alt="image" src="https://github.com/user-attachments/assets/481cd39e-2f50-4bc3-8452-517dbaa067f1" />  

默认情况下，直接使用`routel`命令会显示所有的IPv4路由，默认情况下显200条路由，超出部分可使用 `空格` 下翻，`Ctrl + c` 结束（就如同网络设备一样，为了防止路由过多导致单次查询消耗太多的cpu）  

------------------------------------------------------------------

**可以使用的参数：**  

1、routel -i ：筛选某条路由  

```bash
root@SoftRouting:~# routel -i 192.168.10.0/24
Dst              Gateway  Prefsrc         Protocol  Scope  Metric  Dev  Table
-----------------------------------------------------------------------------
192.168.10.0/24  /        192.168.10.254  kernel    link   425     lan  main
```

2、routel -p 2000：指定打印单页的路由数（默认300条）  

```bash
root@SoftRouting:~# routel -p 2000
```

3、routel -4/-6：指定查询IPv4/IPv6路由  

```bash
routel -6
Dst                      Gateway                   Prefsrc  Protocol  Scope   Metric  Dev              Table
------------------------------------------------------------------------------------------------------------
240e:b8f:2578:2d00::/64  /                         /        ra        global  100     eth0             main
fe80::/64                /                         /        kernel    global  256     tun0             main
fe80::/64                /                         /        kernel    global  1024    eth0             main
fe80::/64                /                         /        kernel    global  1024    lan              main
default                  fe80::11ad:7cc9:26ef:5ce  /        ra        global  100     eth0             main
local                    /                         /        kernel    global  0       lo               local
local                    /                         /        kernel    global  0       eth0             local
local                    /                         /        kernel    global  0       tun0             local
local                    /                         /        kernel    global  0       eth0             local
local                    /                         /        kernel    global  0       lan              local
multicast                /                         /        kernel    global  256     eth0             local
multicast                /                         /        kernel    global  256     eth1             local
multicast                /                         /        kernel    global  256     lan              local
multicast                /                         /        kernel    global  256     eth2             local
multicast                /                         /        kernel    global  256     wlx0013ef6f25bd  local
multicast                /                         /        kernel    global  256     tun0             local
```

4、使用 `空格` 翻页，`Ctrl + c` 结束进程  

5、routel -t：指定查询表的名称（默认显示所有表）  

```bash
root@SoftRouting:~# routel -6 -t local
Dst                                     Gateway  Prefsrc  Protocol  Scope  Metric  Dev              Table
---------------------------------------------------------------------------------------------------------
::1                                     /        /        kernel    host   0       lo               local
240e:b8f:2578:2d00:62be:b4ff:fe02:1360  /        /        kernel    host   0       eth0             local
fe80::366c:2e0d:f39b:36eb               /        /        kernel    host   0       tun0             local
fe80::62be:b4ff:fe02:1360               /        /        kernel    host   0       eth0             local
fe80::af16:e3d1:f0a8:9752               /        /        kernel    host   0       lan              local
ff00::/8                                /        /        kernel    link   256     eth0             local
ff00::/8                                /        /        kernel    link   256     eth1             local
ff00::/8                                /        /        kernel    link   256     lan              local
ff00::/8                                /        /        kernel    link   256     eth2             local
ff00::/8                                /        /        kernel    link   256     wlx0013ef6f25bd  local
ff00::/8                                /        /        kernel    link   256     tun0             local
```

## xfromshow
在使用StrongSwan配置了IPSec VPN后，如果要查看xfrom策略，可使用 `ip xfrom policy` 命令，但显示出的内容过于混乱，因此我写了个脚本可以更直观的显示xfrom策略  

使用时，将我存储库中的xfromshow下载至 `/usr/bin/` 目录下，使用 `chmod + x /usr/bin/xfromshow` 命令添加可执行权限，重新登录后即可使用，效果如下 

------

<img width="1477" height="710" alt="image" src="https://github.com/user-attachments/assets/e7667d96-9b52-43b7-b08a-5755d7a73fec" />

