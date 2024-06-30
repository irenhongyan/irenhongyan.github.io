---
title: git克隆指定秘钥
date: 2024-06-30 17:28:00
categories: # 只有一个
tags: # 多个
keywords: # seo用
top:   # 是否置顶
cover: #是否加入滚翻图
summary: # 如果加密了，那一定要用摘要把默认的去掉
password: # SHA256 加密后的密码
mathjax: # 如果有数学公式需要开启
---

其实我们往往会遇到这样一个问题
打个比方：
> 公司邮箱是：xxx@a.com
个人邮箱：xxx@b.com & xxx@c.com
我们分别有：公司git仓库 / github仓库 / gitee仓库
三个邮箱分别有：id_a_rsa / id_b_rsa / id_c_rsa 三个密钥
三个仓库对应三个不同的邮箱

那么问题来了，我们这三个仓库都需要用ssh 方式来操作git。咋办？

ssh连接默认用的都是 /.ssh目录下的 id_rsa这个密钥，那么我们能不能指定不同的仓库用不同的密钥呢？

# 方法一：
修改/创建 /.ssh/config文件
例：
``` bash
Host github.com #git项目里面的域名
  User git                        # 克隆用户
  Hostname github.com
  PreferredAuthentications publickey
  IdentityFile /opt/aliyun_ssh_key/id_rsa # 私钥路径
  IdentitiesOnly yes
```
这个方法怎么说呢，可行但是个人感觉成本有点高，每次复制git的ssh链接之后需要修改链接里对应的host
如果说你有多个github账号那就要拟定不同的host，其实蛮烦的，而且一旦账号多了可能记不住。
个人并不太喜欢这方法，但是永久性上来说，这是最好的

# 方法二：
这是我在网上搜了2天之后发现的
使用ssh-add命令将对应的key加入到高速缓存中
就以开头的例子为例：
```bash
ssh-add id_a_rsa
ssh-add id_b_rsa
ssh-add id_c_rsa
```
然后 我们分别测试一下git的ssh链接
```bash
ssh -T git@github.com
ssh -T git@gitee.com
```
看看结果吧～

如果不记得自己加入了哪些密钥，只需要使用ssh-add -l命令就可列出所有已加入高速缓存的密钥了
但是唯一的缺陷就是，这只是单次的，电脑重启之后，缓存就会失效，需要重新添加，当然也可以直接编写自动化脚本，每次重启电脑之后自动添加

> 转载自 [美兰十三的想疗院](https://lunashu.org/git-clone-ssh-key/)