---

layout: post
title: linux_ssh_github
tags: [linux, ssh, gtihub]
---

# 在Linux中配置ssh密钥,在Git中使用SSH协议访问Github

在Linux中配置[ssh](https://so.csdn.net/so/search?q=ssh&spm=1001.2101.3001.7020)密钥,在Git中使用SSH协议访问Github，使用 SSH 协议, 您可以连接并验证远程服务器和服务。在每次访问时连接到 GitHub 而不提供用户名或密码。

## 第一步：检查是否存在SSH[秘钥](https://so.csdn.net/so/search?q=%E7%A7%98%E9%92%A5&spm=1001.2101.3001.7020)

1.  Enter `ls -al ~/.ssh` to see if existing SSH keys are present
2.  如果显示`ls: 无法访问/home/qy/.ssh: 没有那个文件或目录` 表示目录不存在，ssh不存在

## 第二步：生成 SSH key.

1.输入指令：

```
$ ssh-keygen -t rsa -C "your_email@example.com"
```

注意：字母C要大写，如下图所示：
![](https://cdn.jsdelivr.net/gh/darkchoco10099/img/20171223004708515)

2、生成[密钥](https://so.csdn.net/so/search?q=%E5%AF%86%E9%92%A5&spm=1001.2101.3001.7020)
![这里写图片描述](https://cdn.jsdelivr.net/gh/darkchoco10099/img/20171223005112294)

```
Enter file in which to save the key (/home/qy/.ssh/id_rsa):  【按回车】
Enter passphrase (empty for no passphrase): 【输入密码】
Enter same passphrase again: 【再次输入密码】
```

如上图所示，到此为止，已经生成私钥和公钥，存储路径如下所示：

```
Your identification has been saved in /home/qy/.ssh/id_rsa.
Your public key has been saved in /home/qy/.ssh/id_rsa.pub.
```

## 第三步:添加 SSH key到 ssh-agent

1、首先确保ssh-agent 工作

```
$ eval $(ssh-agent -s)
Agent pid 8569
```

2、将 ssh 私钥添加到 ssh 代理中。如果使用不同的名称创建了密钥, 或者添加了具有不同名称的现有密钥, 请用私钥文件的名称替换该命令中的 id\_rsa。

```
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/qy/.ssh/id_rsa: 【输入密码】
Identity added: /home/qy/.ssh/id_rsa (/home/qy/.ssh/id_rsa)
```

## 第四步：添加一个新的 SSH key到你的[Github](https://so.csdn.net/so/search?q=Github&spm=1001.2101.3001.7020)账户

1、复制 SSH key 到你的剪贴板

```
$ clip < ~/.ssh/id_rsa.pub
# Copies the contents of the id_rsa.pub file to your clipboard.
```

或者直接打开`~/.ssh/id_rsa.pub` 文件，复制里面的内容
2、添加一个新的 SSH key到你的Github账户
登录你的github，头像处下拉框选择`settings`。
进入设置页后点击侧边栏的`SSH and GPG keys`按钮。
点击`New SSH key`, `title`可以任意填，并且将上一步骤复制的内容粘贴到这里的key输入框中
如果出现提示, 请确认您的 GitHub 密码。

## 第五步：确认

1、输入：

```
$ ssh -T git@github.com
```

2、显示以下内容

```
The authenticity of host 'github.com (192.30.255.113)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.255.113' (RSA) to the list of known hosts.
Hi Qing-Yu-1! You've successfully authenticated, but GitHub does not provide shell access.
```

看到下面这段说明大工告成：

```
Hi Qing-Yu-1! You've successfully authenticated, but GitHub does not provide shell access.
```

更多信息参考：
[https://help.github.com/articles/connecting-to-github-with-ssh/](https://help.github.com/articles/connecting-to-github-with-ssh/)
[https://www.gitbook.com/book/bingohuang/progit2/details](https://www.gitbook.com/book/bingohuang/progit2/details)