title: Linux 常用命令
date: 2018-01-03
author: 张天军
category: 技术文章
tags: [linux]
photos: [https://ws4.sinaimg.cn/large/006tNc79ly1fo1834x7dcj30h80dhjs2.jpg]
---
​	本篇文章用于记录个人学习 Linux 时的比较，分享出来便于记忆和使用。

### Linux 常用命令：

- grep 是在内容里搜索，添加 | 代表扔到管道里面找
  <!--more-->
- which/where 查看命令在哪里
- find 是按文件名/大小/权限搜索 
    1. find ./ -name ".sh"
    2. find ./ -size +4k -size -5M
    3. find /temp -perm 777
- tar 比 zip 压缩内存小
    1. tar -cvf test.tar *.py  (create visibile file) //打包
    2. tar -xvf test.tar (extract visibile file)      //解包
    3. tar -zcvf test.tar.gz *.py                     //打包压缩
    4. tar -zxvf test.tar.gz                          //解压缩
    5. tar -jcvf test.tar.bz2 *.py                    //打包压缩
- cal       日历
- date      当前时间
- ps        查看进程 -a -u -x -w -r (top htop)
- kill      杀死进程 -9
- df        查看内存 dF -h
- du        查看当前路径内存 du -h
- ifconfig  查看ip地址信息（lo 本地回流）
- ifconfig  en4 102.123.21.1 修改ip（windows 修改网关ip）
  ping      
- useradd   添加账户 useradd shuaige -m
- passwd    为账户设置密码 passwd shuaige
- exit      退出当前用户
- whoami    打印当前用户
- ssh       远程控制用户  ssh shuaige@192.123.12.2
- su        切换账户  su shuaige，su - shuaige (- 切换目录)
- who       打印哪些用户登录当前账户
- exit      退出登录当前用户
- userdel   删除账户 userdel shuaige， userdel -r gebilaowang (删除家目录)
- sudo -s   切换到 root 账户 权限最大
- groupadd  添加组
- groupdel  删除组
- groupmod  查看组(连续两次 tab)
- chgrp     修改组 chgrp YYY 1.py 将文件修改到 YYY 组内
- chwon     修改拥有者 chown XXX 1.py 
- cat /etc/passwd 查看密码
- cat /etc/group  查看组
- sudo usermod -a -G sudo 用户名      允许用户执行 sudo 操作
- sudo usermod -a -G adm  用户名      将用户加入到 adm 组内
- `-rw-r--r--  1 jungletian  staff    80B  1  3 18:56 1.py`
    1. jungletian 代表文件拥有者，staff 代表用户组，rw 代表文件拥有者权限 r- 代表同组者权限，r- 其他人的权限，第一个 - 代表这个是文件(drw-r--r-- 是文件)
    2. -rwxrwxrwx -> 文件可读可写可执行
    3. drwxrwxrwx -> 文件夹可读可写可执行
    4. u  g  o  每3个字母代表一个组的权限 u = user; g = group; o = other
    5. 如 chmod u=rwx,g=r,o= 2.py

### vi 使用常用命令：
#### 命令模式输入 
- i  在字符前插入
- I  在行首插入
- o  在下一行插入
- O  在上一行输入
- a  在字符后面插入
- A  在行末尾插入

- yy  复制光标所在行
- dd  剪切光标所在的行
- p   粘贴
- 4yy 复制光标所在行向下4行
- 2dd 前切光标所在行向下2行
- h 前 l 后 j 下 k 上
- H 屏幕上 M 屏幕中 L 屏幕下
- ctrl + f 向下翻一页
- ctrl + b 向上翻一页
- 20 + G 快速定位到第20行
- G 定位到行末
- w 向后跳一个单词的长度
- b 想前跳一个单词的长度
- D 当前光标开始剪切到行末
- u 撤销当前操作
- ctrl + r 反撤销
- d + 0 从当前光标开始剪切到行首
- x 向后剪切当前光标所在位置
- X 向前剪切当前光标所在位置
- v + j/k 多行选中
- V 光标选中当前行
- << 向左移动
- >> 向右移动
- .  重复上次命令
- dw 剪切单词
- r  替换一个字符
- R  替换光标以及后面的字符
- /hello 搜索单词 n 下个出现的位置 N 上个出现的位置
- %s/hello/world/g  将所有 hello 替换为 world
- :1,16s/abc/123/g  将1到16行的 abc 替换为 123
- w 保存
- q 退出
- wq 保存退出
- shift + zz 相当于 wq

### 服务器相关
- 备份Ubuntu默认源地址
- sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
- sudo apt-get update
- sudo apt-get install package
- sudo apt-get remove package
- sudo apt-cache search package 搜索软件包
- sudo apt-cache show package 获取包的相关信息，如说明、大小、版本等
- sudo apt-get install package --reinstall 
- sudo apt-get -f install 修复安装
- sudo apt-get remove package --purge 删除包、包括配置文件等
- sudo apt-get build-dep package 安装相关的编译环境
- sudo apt-get upgrade 更新已安装的包
- sudo apt-get dist-upgrade 升级系统
- sudo apt-cache depends package 链接使用该包依赖哪些包
- ftp 服务器
- samba 服务器 win+r 输入 //192.168.2.1
- ssh 服务器 远程登录
