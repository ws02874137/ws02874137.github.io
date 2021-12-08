## 如何搭建自己的HK VPS

购买vps看自己矿机数量和能力，最低配置即可，矿机流量很小，基本上1K一台的流量计算即可，比如你买1M的带宽，理论上可以带动1千台矿机，当时也最好给自己留点余量。
我推荐有十来台矿机的可以买下面的第二个1核2G/2M带宽，矿机数量超过100台建议购买第三个。Vps一定要购买HK的服务器，以防国外矿池全部进墙，这样买了国内vps也不能访问墙外矿池。

下面仅以Ucloud的vps为例子，其他vps请自行参考相关网站设置
- 通过以下链接可以注册：[点我注册](https://passport.ucloud.cn/?invitation_code=C1x00211FEE83A6)
```markdown
https://passport.ucloud.cn/?invitation_code=C1x00211FEE83A6
```
- 打开[ucloud网站](https://www.ucloud.cn/site/active/kuaijie.html?invitation_code=C1x00211FEE83A6E#xianggang)
```markdown
https://www.ucloud.cn/site/active/kuaijie.html?invitation_code=C1x00211FEE83A6E#xianggang
```
（感谢通过推广链接注册）
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image001.png)

- 上面这个，个人建议直接购买1年或者3年，如果矿机多，选择第三个，新用户2M带宽一年费用是560块左右。
点击购买，下面以我自己购买的2核4G 2M带宽为例来说明。
选择个人新用户，选择1年/3年，点击购买，弹出如下：
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image002.png)
- 注意选择HK地区，安装Windows/Windows 2019 64位，建议高配选择2M带宽，设置好自己的密码，点击立即支付，通过你自己的方式支付完成就购买成功了。

### 设置防火墙
购买完成之后，会提示进入控制台，你也可以登录之后自己打开控制台，控制台左边有两个图标，第一图标是你的主机，第二个图标是网络安全配置。

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image003.png)
- 这样主机就算安装成功了，下面进行远程桌面连接，通过mstsc微软自带桌面连接，如下：

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image004.png)

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image005.png)

- 在这个对话框输入你的公网IP地址，如何查找公网IP地址（后面所有使用的IP地址都是这个），请到UC的网站这里查找：

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image006.png)

- 输入公网IP地址后，弹出输入用户密码和口令对话框，用户输入账号administrator，密码是你在上面购买时候设置的密码，成功之后就远程登录到你购买的vps了。

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image007.png)

- 然后就出现了远程桌面，远程桌面可以把本地文件拷贝，在远程桌面上直接粘贴。

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image008.png)

- 缺省状态下，vps只开放了远程端口和80，443这些，我们还需要开放MinerProxy用到的端口，进入网页控制台，点击左边第二个图标，选择外网防火墙，点击创建防火墙，如下：

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image009.png)

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image010.png)

- 点击+号进行开放端口添加，注意，RDP-3389一定要打开

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image011.png)

- 上面这个ICMP开放，你就可以在ping同这台服务器了，开放快捷规则-RDP，这个是远程桌面连接端口，务必选择。然后把MinerProxy需要的端口放进去，最后点击确认：

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image012.png)

- 这样，自己的防火墙规则创建好了，然后需要把这个规则给你的主机，点击左侧第一个图标

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image013.png)

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image014.png)

- 至此，防火墙就建立好了，然后开始安装MinerProxy

### 安装MinerProxy
下载MinerProxy到本地或者在vps上打开链接下载
```markdown
https://github.com/MinerProxy/MinerProxy/releases/download/1.0.32/MP32_2021_12_06.zip
```
通过远程桌面拷贝MinerProxy到vps服务器：
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image015.png)

- 双击打开MinerProxy，选择自己需要的矿池，点击开始运行:

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image016.png)

### 设置矿机连接
下面是矿机连接自己的矿池代理设置，你可以把这个代理当做一个矿池来使用：
- 注意将{host}改为运行代理的矿机IP地址或者主机名
- 将{wallet}更改为您自己的钱包，{worker}更改为您自己的矿机名称
- 比如我的IP地址为192.168.1.8，那么gm需要这样连接：
```markdown
miner --algo ethash --server 192.168.1.8:3333 --user 0xabcxxxxxxxxxxx.myworker
```
**GMiner连接**
- TCP端口方式：
```markdown
miner --algo ethash --server {host}:3333 --user {wallet}.{worker}
```
- SSL加密连接方式：
```markdown
miner --algo ethash --server {host}:14333 --user {wallet}.{worker} --ssl 1
```

**NBMiner连接**
- TCP端口方式：
```markdown
nbminer -a ethash -o stratum+tcp://{host}:3333 -u wallet.worker --log
```
- SSL加密连接方式：
```markdown
nbminer -a ethash -o stratum+ssl://{host}:14333 -u wallet.worker --log
```

**T-REX连接**
- TCP端口方式：
```markdown
t-rex.exe -a ethash -o stratum+tcp://{host}:3333 -u {wallet} -p x -w {worker}
```
- SSL加密连接方式：
```markdown
t-rex.exe -a ethash -o stratum+ssl://{host}:14333 -u {wallet} -p x -w {worker} --no-strict-ssl
```

**各种挖矿软件，OS系统**
- 挖矿软件请在矿池管理添加一个矿池，矿池地址如下：
- TCP方式： {host}:3333
- SSL方式:  {host}:14333

内核连接VPS SSL 1433端口，举例如下：
- 假设远程VPS的IP地址为112.112.112.112，SSL端口设置为14333
- 直接内核GM的BAT文件连接方式：
```markdown
miner --algo ethash --server 112.112.112.112:14333 --user 0x888xxxx.myrig --ssl 1
```
- 内核NB的BAT直接连接方式：
```markdown
nbminer -a ethash -o stratum+ssl://112.112.112.112:14333 -u 0x888xxx.myrig --log
```

**轻x矿工的连接方式，请增加一个矿池，设置如下：**

![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image017.png)

- 其中矿池地址设置为： stratum+ssl://112.112.112.112:14333

- 另外注意，开x矿工不支持NB 内核的SSL自定义矿池，唯一办法就是本地安装MP，开X通过TCP连接到本地MP，再通过本地MP使用SSL方式连接到VPS的MP。
- 开X矿工如果试用Gminer内核，可以按照普通方式增加112.112.112.112:14333矿池，然后在高级设置里面增加 --ssl 1

**凤凰矿工如何连接VPS**
- 由于凤凰对于ssl的连接需要进行证书校验，通过IP地址连接是无法通过证书校验的，所以需要在本地hosts加入VPS 的IP地址映射到域名：
```markdown
proxy.wiseminer.top
```
- 在windows下，打开c:\windows\system32\drivers\etc\hosts. 这个文件，加入IP和域名映射，请将下面xxx.xxx.xxx.xxx改为你的vps的公网IP地址：
```markdown
xxx.xxx.xxx.xxx   proxy.wiseminer.top
```
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image018.png)
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image019.png)
- 请注意将上面的118.193.38.188更改为自己的VPS的公网IP地址！！！

- OS等Linux系统如何加入域名映射：
- 如果有路由器的，比如openwrt，请在高级设置中加入dns域名：
![Image](http://s-gz-416-dmgf-dl.oss.dogecdn.com/Ucloud/image020.png)

- 其他路由器，请自行设定，由于HiveOS系统 /etc/hosts会被自动覆盖，故在OS系统强行增加域名映射之后，重启会被覆盖，所以请自行想办法。

### 查看收益
- 比如上面我设置的矿池是asia2.ethermine.org，你可以直接打开网址
https://www.ethermine.org/
然后输入自己的钱包地址，查看收益状态。
- 注意!
- ethermine需要15分钟同步数据。


### 如果觉得麻烦也可以直接使用现成搭建好的中转
- ethermine池-SSL-HK中转-抽水0.35%
```markdown
ethermine.hk.mio.cool:5555
```
- ethermine池-SSL-HK中转-抽水0.35%
```markdown
2miners.hk.mio.cool:12020
```
- 必须开启SSL 你懂的
