www.github.com



注册

### 新建项目

 1. 项目名

 2. 描述

 3. 勾上ReadMe

 4. 自动添加java

    生成两个文件

    .ignone

    .ReadMe

### git操作

​	下载连接http://npm.taobao.org/mirrors/git-for-windows/

cmd清屏cls

文件夹右键在这里打开cmd

新建文件OpenCmdHere.txt

~~~reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\OpenCmdHere]
@="cmd_here"
"Icon"="cmd.exe"

[HKEY_CLASSES_ROOT\Directory\shell\OpenCmdHere\command]
@="cmd.exe /s /k pushd "%V""

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCmdHere]
@="cmd_here"
"Icon"="cmd.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCmdHere\command]
@="cmd.exe /s /k pushd \"%V\""

[HKEY_CLASSES_ROOT\Drive\shell\OpenCmdHere]
@="cmd_here"
"Icon"="cmd.exe"

[HKEY_CLASSES_ROOT\Drive\shell\OpenCmdHere\command]
@="cmd.exe /s /k pushd \"%V\""

[HKEY_CLASSES_ROOT\LibraryFolder\background\shell\OpenCmdHere]
@="cmd_here"
"Icon"="cmd.exe"

[HKEY_CLASSES_ROOT\LibraryFolder\background\shell\OpenCmdHere\command]
@="cmd.exe /s /k pushd \"%V\""

~~~

保存修改后缀reg。双击打开，一直确定。

下载到本地

clone-》use ssh复制

在右键打开cmd

git clone 粘贴

没有权限，

添加一个key

setting->ssh and gpg key

生成ssh key

add a new key

genertaing a new ssh

在git中操作

ssh-keygen -t rsa -b 4096 -C "648652898@@qq.com"

clip < ~/.ssh/id_rsa.pub

回到ssh and gpg keys

add new 直接粘贴就好了

到这里可以glone了



新建文件first

git init

git status

git add first

git commit -m "first common"

git config --global user.email  邮箱

git config --global user.name xinhe0616

git status

git log

出错回滚

git reset 复制错误编码到这里

git add .

git commit -m "first common"

git status

git push



修改文件

git add 文件名包括后缀

或者git add .    添加所有文件

git commit -m "添加描述"

git push

当其他人修改了代码就会发生冲突

git pull

下载冲突自动合并文件

修改文件并且把箭头去掉

重新提交



创建分支

git branch branch1

git checkout branch1

提交

没有在远端设置分支

根据提示操作

在网络端有个新分支

两个分支不冲突

git pull

git merge branch1

git push

用idea解决冲突

idea使用git

https://www.cnblogs.com/javabg/p/7987755.html

