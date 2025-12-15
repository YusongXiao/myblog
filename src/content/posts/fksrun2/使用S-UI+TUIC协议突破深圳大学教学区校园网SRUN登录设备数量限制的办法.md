---
title: 使用S-UI+TUIC协议突破深圳大学教学区校园网SRUN登录设备数量限制的办法
published: 2025-12-16
description: 本文讲述了使用S-UI+TUIC协议的方法
# image: ./cover.png
tags: [折腾网络, 吐槽, 技术分享]
category: Blog
draft: false
---


> 注：本文以及本文引用的链接并未教程，只是个人学习的记录，该记录也并未损害任何人的权益
> 部分信息可能由AI生成
# 效果与限制
优点：终端设备无需与出口机处于同一网段（甚至终端设备可以在宿舍区），可以抵抗深度包检测（DPI），此办法永久有效
限制：终端设备需要使用V2ray等程序，延迟不稳定，所有终端设备出口ip均为出口机

# 需要的设备

一台linux机器

# 配置
## 联网
Linux Desktop直接[net.szu.edu.cn](https://net.szu.edu.cn)
Linux Server可以使用[Caterpie771881/szu_srun_client](https://github.com/Caterpie771881/szu_srun_client)
联上网之后如果以后不想自己手动登录可以使用[YusongXiao/szu_srun_client](https://github.com/YusongXiao/szu_srun_client)

## 安装S-UI

假设Linux ip是192.168.239.100

参考了[【不良林】技术分享](https://bulianglin.com/archives/nicename.html)

```bash
VERSION=1.2.2 && bash <(curl -Ls https://raw.githubusercontent.com/alireza0/s-ui/$VERSION/install.sh) $VERSION
```
安装过程中出现y/n时，直接点回车就好
用户名和密码会生成在控制台
安装完毕访问192.168.239.100:2095

## 配置Tuic+tls

TSL设置 -> 添加 -> TLS -> 生成证书（钥匙按钮） -> 启用允许不安全 -> TLS选项（ALPN, SNI） -> SNI:net.szu.edu.cn
![](./assets/20251230231241.png)

然后点击入站管理，照下面配置
![](./assets/20251231231219.png)

## 使用
点击用户管理，添加TUIC节点
![](./assets/20251233231209.png)
保存之后点击查看二维码
![|401x440](./assets/20251237231245.jpg)
点击二维码可以获得类似以下信息
```
tuic://24b0eaf3-b781-4dbd-92d8-50ab18ba5f8b:Zl8Qp7l9CN@192.168.239.100:8443?alpn=h3%2Ch2%2Chttp%2F1.1&congestion_control=bbr&insecure=1&sni=net.szu.edu.cn#tuic-48132
```



# 终端设备的配置

## 电脑
Windows，Linux Desktop，Macos可使用V2rayN

使用[Release 7.16.6 · 2dust/v2rayN](https://github.com/2dust/v2rayN/releases)
直接ctrl+v刚才的节点信息
系统代理（自动配置系统代理）
路由（全局）
即可

## 手机
Android使用V2rayNG
Apple使用ShadowSocks

## 其他终端
比如Linux Server使用sing-box


