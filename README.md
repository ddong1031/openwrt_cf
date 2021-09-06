# 自动替换 PassWall 里面的 WS 节点地址 为 CF 优选的IP
## 新增微信推送 杀脚本命令


用途：用于自动筛选 CF IP，并自动替换优选 IP 为 PassWall 的节点地址，并将结果推送到微信

本脚本源于 GitHub：Lbingyi Paniy 波仔 xiaofeng

## 使用说明

在使用passwall的基础上，太老版本不支持，看节点是否有 option tcp_node id字段，懂点基础的也可以根据id，参数等节点自行修改脚本（思路无非是通过id找节点）

* 输入命令 vi /etc/config/passwall 信息里面的 config global —— option tcp_node 后面的字符串，为你正在使用的自定义节点的绑定字符串 

> 关于 vi 的相关操作：
按键盘上面的 PgUp 和 PgDn 进行翻页，按 i 键进行编辑，按 esc 退出编辑，按 :wq 保存并退出 vi 命令

* 在软路由里面下载 cf-auto-passwall 脚本

> ``wget https://raw.githubusercontent.com/ddong1031/openwrt_cf/main/cf-auto-passwall.sh``
>> 已经下载用过之前脚本的请使用命令``ls``查看是否存在重名脚本，并使用``rm cf-auto-passwall.sh``删除当前重名文件后重新运行``wget https://raw.githubusercontent.com/ddong1031/openwrt_cf/main/cf-auto-passwall.sh``

> 下载后，脚本的绝对地址为 /root/cf-auto-passwall.sh

* 添加微信推送

>> pushplus API接口申请地址：[点击进入](https://pushplus.hxtrip.com) 微信扫码登录获取token

>> ![示例](https://wxf2088.xyz/wp-content/uploads/2021/02/1612271787-3f6482561574dfa.jpg)

>> 选择一对一推，记录你的微信token，稍后会在脚本中用到

* 编辑该脚本

>> vi cf-auto-passwall.sh
>> 更改相关的参数（默认优选带宽大小 字段 ``bandwidth``、节点相对应的字符串），并保存
>>> passwall 节点id替换 ``xxxxxxxxxx`` 微信的token 替换最后curl开头的``你的id``


* 软路由运行下，看看出没出错。

> ``chmod +x cf-auto-passwall.sh && bash cf-auto-passwall.sh``
> 运行完会在优选完ip之后 及时推送到微信中 此时查看passwall中的节点地址已经替换

* 加在 openwrt 上系统 计划任务里 添加定时运行

> 如 0 4 * * 2,4,6 bash /root/cf-auto-passwall.sh > /dev/null
> 0 4 * * 2,4,6 的意思是在每周二、周四、周六的凌晨4点会自动运行一次。/root/cf-auto-passwall.sh 是你脚本的绝对地址

* 如果存在死循环问题 可以下载杀脚本命令 并添加到计划任务中

> 脚本 地址 ``wget https://raw.githubusercontent.com/ddong1031/openwrt_cf/main/kill-cf-auto-passwall.sh``

> 计划任务 在 设定完优选IP后 建议在5-10分钟左右 执行``5 4 * * * bash /root/kill-cf-auto-passwall.sh > /dev/null`` 如果怕没权限 可以下运行一下``chmod +x kill-cf-auto-passwall.sh``赋予权限

> 时程表的格式如下:
> 
> f1 f2 f3 f4 f5 program
> 
> 其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执行的程式。
>
> 0 03 * * * 表示每天的凌晨三点


# 喜欢点个Star，自用 定期更新

## 注意事项

1、请在脚本中修改你期望优选 IP 的带宽大小（默认50M）

2、请替换 426行``passwall.xxxxxxxxxx.address=$anycast``中xxxxxxxxxx 字符串为你自己 PassWall 的节点值

3、微信推送 替换 428行``curl -s -o /dev/null --data "token=你的id&`` 中你的id 替换为你自己的微信token

4、杀脚本命令 通常没有必要 如果 出现一直 等待icmp进程结束 剩余进程数 说明固件缺少命令包 请换固件或者尝试下载完整命令包 例如brew等自行google

## 网址借鉴 

* 波仔 https://github.com/V2RaySSR/cf-auto-passwall 视频 https://www.youtube.com/watch?v=WzRHi9f9QKg

* 脚本源 badafans https://github.com/badafans/better-cloudflare-ip

* xiaofeng https://wxf2088.xyz/2582.html 视频 https://www.youtube.com/watch?v=Cs1V0qv9UYo
