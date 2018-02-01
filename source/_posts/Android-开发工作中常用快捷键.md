title: Android 开发工作中常用快捷键
date: 2017-12-15 21:20:48
author: 张天军
category: 技术文章
tags:
- android
- 开发工具
photos: [https://ws3.sinaimg.cn/large/006tNc79ly1fmhrt0pi0zj3074074dg5.jpg]
---


### **Android 开发常用 adb 命令**

adb 命令 | 描述
---|---
`adb logcat -v time > log.txt` | 打印 log 并保存到文件里
`adb shell dumpsys activity top` | 查看最顶层 Activity 元素
`adb shell dumpsys activity activities` | 查看栈内的信息 参数可选为 `sed -En -e '/Stack #/p' -e '/Running activities/,/Run #0/p'`
`adb shell dumpsys activity grep -i run` | 查看正在运行的 Activity
`adb shell pm clear <package_name>` | 清除应用缓存
`adb shell am set-debug-app -w <package_name>` | 设置指定应用为 debug 模式
`adb shell am start -S -W  <package_name>/<package_name>.Activity` | 计算 Activity 启动耗时
`adb shell am start -n yourpackagename/.activityname` | 新打开一个 activity
`pidcat com.Qunar -t <tag_name>` | `pidcat` 查看指定进程的 TAG 的日志
`adb shell screencap /sdcard/screenshot.png` | 截屏
`adb pull /sdcard/screenshot.png ./` | 拉取文件
`adb shell rm /sdcard/screenshot.png` | 删除文件
`adb shell am force-stop <PACKAGE>` | 强制杀死进程
`adb shell am kill [options] <PACKAGE>` | 杀死进程以及关联后台进程
./gradlew assembleDebug --daemon --parallel | 开启 daemon 进程加快编译速度


<!--more-->

### **常用 app 快捷键**
| 命令                                      | 描述                    |
| ---------------------------------------- | --------------------- |
| iterm2 : `ctrl + [ or ]`                  | 切换 pane               |
| iterm2 : `ctrl + k`                      | 命令行光标之后的              |
| iterm2 : `ctrl + a`                      | 命令行光标移到首字母            |
| chrome : `command + alt + -> or <-`       | 切换 chrome tab         |
| finder : `command + shift + g`           | 输入 /etc 进入            |
| terminal : `sudo vi /etc/hosts `         | 修改 hosts 文件           |
| terminal : `sudo chown -R user /xxx/aaa/` | 修改权限                  |
| terminal : `defaults write com.apple.finder AppleShowAllFiles -boolean true; killall Finder` | true 显示隐藏文件，false 则相反 |
| sublime : `ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime` | 设置 sublime 允许在命令行种启动  |
| 选中文件右键-显示简介-打开方式-全部更改                    | 默认打开某格式文件             |

### **Android Studio 快捷键**

| 快捷键                                      | 描述              |
| ---------------------------------------- | --------------- |
| `command + shift + delete`               | 上一个编辑的位置        |
| `command + 单击 tab`                       | 在外部打开文件         |
| `alt + space / command + y`              | 快速查看定义          |
| `command + shift + e`                    | 最近修改的文件         |
| `command + alt + p`                      | 提取参数            |
| `command + alt + t`                      | 代码包裹            |
| `command + shift + delete`               | 移除包裹            |
| `alt + F10`                              | 显示当前运行点(Debug时) |
| `ctrl + g`                               | 显示并选中下一个调用的地方   |
| `ctrl + tag`                             | 切换窗口并选中         |
| `studio diff <file_name_1> <file_name_2>` | AS 文件对比         |
| `code --diff <file_name_1> <file_name_2>` | vs code 文件对比    |

### **Linux 系统常用命令 **

命令 | 描述
---|---
`ln -s <source_file> <link_file_name>` | 创建快捷方式(-s 软链接 默认是硬链接)
`cat <file_name>` | 查看文件
`cat <file_name> <file_name2> > <file_name3>` | 将两个文件内容复制到另外一个文件
`touch <file_name>` | 创建文件
`grep -n "^word"/"word$" <file_name>` | 在指定文件里面搜索单词(-n: 显示行数；-v：不包含 `word` 的单词)
`cp <folder_name> <folder_name2> -r ` | 拷贝文件夹

### **调试技巧**

    调试状态下，按住Alt键，然后单击表达式即可
    右键需要填写表达式的断点，然后输入布尔表达式
    在断点上右键，取消Suspend的勾选，然后勾选上Log evaluated Expression，并在输入框中输入你要打印的日志信息。

