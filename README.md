# V2ray for Koyeb

* * *

# 目录

- [项目特点](README.md#项目特点)
- [部署](README.md#部署)
- [鸣谢下列作者的文章和项目](README.md#鸣谢下列作者的文章和项目)
- [免责声明](README.md#免责声明)

* * *                                             

## 项目特点:（可以用在NF，《免费容器NorthFlank搭建V2教程https://iweec.com/880.html》）   
* 本项目用于在 Koyeb 免费服务上部署 V2ray ，采用的方案为 Nginx + WebSocket + VMess/VLess + TLS。
* V2ray 核心文件和配置文件作了“特殊处理”，每个项目都不同，大大降低被封和连坐风险
* vmess 和 vless 的 uuid，路径既可以自定义，又或者使用默认值
* 集成哪吒探针，可以自由选择是否安装
* 部署完成如发现不能上网，请检查域名是否被墙，可使用 Cloudflare CDN 或者 worker 解决。

## 部署:
* 注册 [Koyeb.com](https://app.koyeb.com/auth/signin/)
* [![Deploy to Koyeb](https://www.koyeb.com/static/images/deploy/button.svg)](https://app.koyeb.com/deploy?type=docker&name=v2r&ports=80;http;/&env[UUID]=de04add9-5c68-8bab-950c-08cd5320df18&env[NEZHA_SERVER]=server%20domain%20or%20ip&env[NEZHA_PORT]=server%20port&env[NEZHA_KEY]=agent%20key&image=docker.io/fscarmen/v2-koyeb) |
* 可用到的变量
  | 变量名 | 是否必须 | 默认值 | 备注 |
  | ------------ | ------ | ------ | ------ |
  | UUID         | 否 | de04add9-5c68-8bab-950c-08cd5320df18 | 可在线生成 https://www.zxgj.cn/g/uuid |
  | VMESS_WSPATH | 否 | /vmess | 以 / 开头 |
  | VLESS_WSPATH | 否 | /vless | 以 / 开头 |
  | NEZHA_SERVER | 否 |        | 哪吒探针服务端的 IP 或域名 |
  | NEZHA_PORT   | 否 |        | 哪吒探针服务端的端口 |
  | NEZHA_KEY    | 否 |        | 哪吒探针客户端专用 Key |

![image](https://user-images.githubusercontent.com/92626977/211201128-8eb8c495-03b1-4837-b11d-db5d5cf37a10.png)
![image](https://user-images.githubusercontent.com/92626977/211201164-51917877-c672-4b62-9031-67b497fd0936.png)
![image](https://user-images.githubusercontent.com/92626977/211201178-386d8e2c-189b-40ba-a37f-ebcd4ae2be5e.png)
![image](https://user-images.githubusercontent.com/92626977/211201189-62649d0d-ebb0-42f4-946a-38dea2601b46.png)
![image](https://user-images.githubusercontent.com/92626977/211201196-3d7e59ae-3b55-42db-81ac-b324d60a0bb1.png)
![image](https://user-images.githubusercontent.com/92626977/211201217-6a5c9493-4aa9-4c68-9cba-966893617ab0.png)

=================================================================
免费容器NorthFlank搭建V2教程 免费容器NorthFlank搭建V2教程
 梅塔沃克  2023-05-22 PM
https://www.youtube.com/watch?v=lQQ4vyI0pmw
NorthFlank使用的是Google云服务器，速度方面还算可以，优势就是：需要绑定信用卡，可以过滤很多人，所以使用的人不太多。

实际测试Youtube最高跑4万，勉强8K，当然不同的网络、不同的时段表现肯定不同，大家可以在视频下方进行反馈！

未标题-1.jpg

简介Northflank
Northflank 是一个云原生应用部署和管理平台，旨在简化开发人员和团队在云环境中部署、扩展和管理应用程序的过程。它提供了一套强大的工具和功能，帮助开发人员更轻松地构建、部署和运行应用。

免费用户需要绑定信用卡（部分虚拟卡可用），默认免费项目可以部署0.2 vCPU / 512MB的应用，而对于V2来说，可以部署2个Node。

本次部署的源码网址： https://github.com/fscarmen2/V2-for-Koyeb ，一看便知是写Koyeb的，不过Koyeb不仅需要绑卡，现在申请需要人工审批，很难申请到，操作方法一致，以后再给大家做Koyeb。

准备工作
1、信用卡一张，最好是实体。我推荐比价新的：https://wenjie.org/archives/card

2、GitHub账号一个；

部署教程
1、首先在 https://app.northflank.com/login 登陆账号，谷歌账号、github是可以直接登陆的。为了简单，我们就直接谷歌登陆吧。

2、然后就是输入用户名，同意协议就可以继续了；
截屏2023-05-22 21.23.23.png

3、当我们要激活默认项目的时候，需要绑定信用卡，自己绑定吧。

4、在 https://github.com/fscarmen2/V2-for-Koyeb 页面，Fork一下项目，别忘了给大佬点个赞。

5、在 northflank个人仪表盘中，点击Git，链接你的github账号，然后就在默认项目中创建新的服务。

6、Service name（随便写）；存储库就选择我们刚刚的；Branch 选择（main）type选择dockerfile 、端口选择：80，其他默认，开始构建；

7、构建完成，访问你的项目地址看到：Welcome to nginx，这里提一下，NorthFlank给到的是有root权限的ssh，用于联系Linux命令也非常不错（弱弱说一下，可以测试一下安装宝塔，我就不测试了）。
截屏2023-05-22 21.47.23.png

8、客户端设置：
网址：你的项目地址
端口：443
UUID：de04add9-5c68-8bab-950c-08cd5320df18
PATH：/vmess 或者/vmess

绑定域名
1、在仪表盘中，可以添加域名：点击添加域名，然后输入你的域名；

2、按照提示进行TXT解析，然后添加cname，验证后即可绑定在项目上；

总结
NorthFlank部署简单，而且暂时没有发现有流量限制，免费的东西可要珍惜了。

==================================================================
## 鸣谢下列作者的文章和项目:
ifeng 的 v2ray 项目，在此基础上作修改 https://www.hicairo.com https://github.com/hiifeng

## 免责声明:
* 本程序仅供学习了解, 非盈利目的，请于下载后 24 小时内删除, 不得用作任何商业用途, 文字、数据及图片均有所属版权, 如转载须注明来源。
* 使用本程序必循遵守部署免责声明。使用本程序必循遵守部署服务器所在地、所在国家和用户所在国家的法律法规, 程序作者不对使用者任何不当行为负责。
