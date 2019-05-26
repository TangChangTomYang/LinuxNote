#### 一、远程管理常用命令

- 关机/ 重启
    - shutdown

- 查看或者配置网卡信息
    - ifconfig
    - ping
- 远程登录和远程复制
    - ssh
    - scp
    
#### 二、关机和重启
|序号| 命令| 对应英文| 作用|
|-|-|-|-|
|01| shutdown 选项 时间| shutdown | 关机/ 重新启动|

**01、shutdown**
- `shutdown 命令可以 **安全关闭或者重启系统**

|选项|含义|
|-r|重新启动|

> 提示
- 不指定选项和参数, 默认表示1分钟之后关闭电脑
- 远程维护时, 最好不要关闭系统, 应该重新启动

```
常用命令

shutdown -r now
// 表示重新启动, 其中 now 表示现在

shutdown now
//立即关机, 其中now 表示现在

shutdown 20:20
// 系统在今天的 20:20自动关机

shutdow +10
// 系统在10分钟后关机

shutdown -c
// 取消之前指定的关机计划
```


<br>
#### 三、 查看或配置网卡信息

|序号|命令|对应英文| 作用
|-|-|-|-|
|01| ifconfig| config a network interface| 查看/ 配置计算机当前的网卡信息|
|02| ping ip地址| ping | 检测到目标ip 地址的网络是否正常|

**01、网卡和IP地址**

**网卡**
- 网卡是一个专门用于负责网络通讯的硬件设备
- IP地址是设置在网卡上的地址信息, 用于唯一标识计算机

> 我们可以把IP地址理解为计算机的身份证号




<br>
**02、ifconfig**
```
ifconfig
// 查看网络配置信息

ifconfig | grep inet
// 查看ipv4的信息, 在Lunix 中inet6 标识的是ipV6地址
```
    
<br>
**03、ping**
- `ping` 一般用于检测网络通不通, 数值越大,速度越慢

> ping 的原理和潜水艇的声呐相似, ping这个命令就取自声呐的声音. 网络上的计算机都有唯一的IP地址, 我们给目标地址发送衣蛾数据包, 对方就要返回一个数据包, 根据返回的数据包即时间, 我们就可以确定目标主机是否存在.





<br>
#### 四、远程登录和复制

|序号| 命令| 对应英文| 作用|
|-|-|-|
|01| ssh 用户名@ip地址| secure shell|以xxx用户的身份远程登录某台电脑|
|02| scp 用户名@ip地址:文件名或路径| secure copy| 远程复制文件|



**01、ssh 基础**
在Linux 中, ssh 是非常重要的工具, 通过ssh 客户端可以连接到运行了 ssh 服务器的远程机器上

```
数据传输是加密的, 可以防止信息泄露
数据传输是压缩的, 可以提高传输速度

ssh 客户端 ---------> ssh 服务端
```

- ssh 客户端是一种使用 `secure shell (ssh)` 协议连接到远程计算机的软件程序
- ssh 是目前较可靠, 转为远程登录会话和其它网络服务提供安全性的协议
    - 利用 `ssh协议` 可以有效的防止远程管理过程中信息的泄露
    - 通过 `ssh协议` 可以对所有传输数据进行加密, 也能防止DNS欺骗和IP欺骗
- ssh 的另一项优点是传输的数据是经过压缩的,所有可以加快传输速度.

<br>
**02、域名和端口**
- 域名: 由一串由点分割的名字组成, 例如: `www.baidu.com` 是 `ip地址`的别名, 方便记忆.
- 端口号: 通过IP地址找到网络上的计算机, 通过端口号可以找到计算机运行的 响应的应用程序.
    - ssh 服务器默认的端口号是 `22`, 如果是默认端口号, 在链接的时候可以省略
- 常见的服务器端口号
|序号| 服务| 端口号|
|-|-|-|
|01|ssh 服务器| 22|
|02|web服务器|80|
|03|HTTPS|443|
|04|FTP 服务器| 21|

<br>
**03、ssh 客户端的简单使用**
```
ssh [-p port] userName@remote

如: 
ssh -p 22 zhangsan@192.168.100.1
简写为
ssh zhangsan@192.168.100.1
```
- userName 是远程机器上的用户名, 如果不指定的话默认为当前用户
- remote 是远程机器的ip地址, 可以是ip或域名, 或者是别名
- port  是ssh server监听的端口, 如果不指定默认就是22

> 提示:
- 使用`exit` 退出当前用户的登录

<br>
> 注意:
- `ssh` 这个终端命令只能在`Linux` 或者 `Unix` 系统上使用(苹果也可以)
- 如果在 `window` 系统中,可以安装`Putty` 或者 `XShell` 客户端即可, 用户和ssh 原理是一样的.


<br>
> 提示:
- 在工作中, ssh 服务器的端口很有可能不是 `22`, 如果遇到这样的情况, 就需要使用选项 `-p` 指定正确的端口号即可.



<br>
**04、 window 下 SSH 客户端下载安装**
- `Putty`: http://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

- `XShell`: http://xshellcn.com

建议从官网下载正版



<br>
**05、 scp 远程文件拷贝**

- `scp` 就是 `secure copy` , 是一个在Linux 下用来进行远程拷贝文件的命令
- 他的地址格式与`ssh` 基本相同, 需要注意的是, 在指定端口时, 使用的是大写 `-P` 而不是小写 `-p`

```
文件/目录                         文件/目录
ssh客户端 <----------------------> ssh 服务端
```


**常用命令:**

```
scp -P port 01.txt userName@remote:Desktop/01.txt
// 把本地当前目录下的 01.txt 文件复制到远程主机下家目录的 Desktop/01.txt
// 注意: `:` 后面的路劲如果不是绝对路径, 则以用户家目录作为参照路劲

scp -P port userName@remote:Desktop/01.txt 01.txt
// 把远程 家目录下的 Desktop/01.txt 文件复制到本地当前目录下的01.txt

scp -r demo userName@remote:Desktop
// 把当前目录下的demo 目录复制到远程主机的家目录的Desktop
// -r 表示递归复制目录

scp -r userName@remote:Desktop demo
// 将远程主机家目录下的Desktop 目录拷贝到本地的demo目录下
```

|选项| 含义|
|-|-|
|-r|如果给出烦的源文件是目录, 则scp 将递归复制该目录下的所有子目录和文件,目标文件必须为一个目录|
|-P| 若 远程ssh 服务器的端口不是22, 那么需要使用大写字母 -P 指定端口|



> 注意:
- scp 这个终端命令只能在 `Linux`  或者`Unix` 中使用.(apple 可以)
- 如果在`windows`中, 可以安装`Putty` 使用`pscp`命令行工具, 也可以安装 `FileZilla` 使用`FTP` 协议进行文件传输


**FileZilla**
- 官方网站: https://www.filezilla.cn/download/client
- `FileZilla` 在传输时使用的是`FTP服务` 而不是`ssh服务`, 因此端口号是 `21`



<br>
**06、ssh 高级**

- 免密码登录
- 配置别名
> 提示:
有关SSH配置的相关信息保存在用户家目录下的 `.ssh` 隐藏目录下

**1)、免密码登录**
**步骤: **
- 配置公钥
    - 执行 `ssh-keygen` 即可生成ssh钥匙, 一路回车即可
- 上传公钥到ssh 服务器
    - ssh-copy-id -p port userName@remote  // 可以让远程服务器记住我们的公钥(即保存公钥)
    

![](/assets/Snip20190520_1.png)
> 补充说明: 非对称加密的特点
- 使用 `公钥`加密的数据, 使用`私钥` 解密. 
- 使用 `私钥`加密的数据, 使用`公钥`解密.
 (私钥加密的过程一般称为签名, 公钥解密的过程一般称为验签)
 
<br>
**2)、配置别名**
每次都输入 `ssh -p port userName@remote`, 时间长了会觉得很麻烦. 而配置别名, 可以让我们进一步偷懒, 譬如: 使用 `ssh zhangsanMac` 来代替上面这么一段.

配置别名其实很简单, 只需要在 `~/.ssh/config` 里面追加以下内容即可:
```
Host zhangsanMac
    HostName id地址
    User zhangsan
    port 22
```
保存之后即可使用 `ssh zhangsanMac` 实现远程登录了, `scp` 同样可以使用

>示例:
ssh zhangsanMac // 远程登录到张三的mac
scp -r Desktop zhangsanMac:Desktop/abc // 将当前的桌面,复制到远程zhangsan的mac上.

