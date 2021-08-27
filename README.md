## 自动替换 PassWall 里面的 WS 节点地址 为 CF 优选的IP


用途：用于自动筛选 CF IP，并自动替换优选 IP 为 PassWall 的节点地址

借鉴波仔 www.v2rayssr.com （已开启禁止大陆IP访问）ouTube频道：波仔分享

本脚本源于 GitHub：Lbingyi 以及 Paniy 和 波仔
 
视频演示地址：https://youtu.be/WzRHi9f9QKg

## 使用说明

在使用passwall的基础上，太老版本不支持，看节点是否有 option tcp_node id字段，懂点基础的也可以根据id，参数等节点自行修改脚本

* 输入命令 vi /etc/config/passwall 信息里面的 config global —— option tcp_node 后面的字符串，为你正在使用的自定义节点的绑定字符串 

> 关于 vi 的相关操作：
按键盘上面的 PgUp 和 PgDn 进行翻页，按 i 键进行编辑，按 esc 退出编辑，按 :wq 保存并退出 vi 命令

* 在软路由里面下载 cf-auto-passwall 脚本

> ``wget https://raw.githubusercontent.com/ddong1031/openwrt_cf/main/cf-auto-passwall.sh``

> 下载后，脚本的绝对地址为 /root/cf-auto-passwall.sh

* 编辑该脚本

>> vi cf-auto-passwall.sh
>> 更改相关的参数（默认优选带宽大小、节点相对应的字符串），并保存

* 软路由运行下，看看出没出错。

> ``chmod +x cf-auto-passwall.sh && bash cf-auto-passwall.sh``

* 加在 openwrt 上系统 计划任务里 添加定时运行

> 如 0 4 * * 2,4,6 bash /root/cf-auto-passwall.sh > /dev/null

> 0 4 * * 2,4,6 的意思是在每周二、周四、周六的凌晨4点会自动运行一次。/root/cf-auto-passwall.sh 是你脚本的绝对地址

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

2、请更改 421 行 的 xxxxxxxxxx 字符串，为你自己 PassWall 的节点值

3、如果还不会请看视屏地址 https://youtu.be/WzRHi9f9QKg

## GitHub 地址借鉴 

* 波仔 https://github.com/V2RaySSR/cf-auto-passwall

* badafans https://github.com/badafans/better-cloudflare-ip