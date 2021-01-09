## 运行git 前的配置 ##

Git 自带一个 git config 的工具来帮助设置控制 Git 外观和行为的配置变量。 这些变量存储在三个不同的位 置：

### 1. linux 配置文件位置 ###

``` shel
* . /etc/gitconfig 文件:系统级别  设置时候  --system
* ~/.gitconfig 或 ~/.config/git/config 文件 当前用户 设置时候 -- global
* .git/config  当前仓库 针对该仓库   设置时候 --local
```

### 2. windows 配置文件位置

``` shell
* 安装目录 /etc/gitconfig 文件 设置 --system
* C:\Users\Administrator 文件 设置 --global
* .git/config 当前仓库   设置 --local
```

可以通过命令：

``` git
git config --list --show-origin 查看所有配置

```

## Git配置多个SSH-Key

[SSH Key](https://gitee.com/help/labels/19)

### 背景

当有多个git账号时，比如：

a. 一个gitee，用于公司内部的工作开发；
b. 一个github，用于自己进行一些开发活动；

### 解决方法

1. 生成一个公司用的SSH-Key

```shell
$ ssh-keygen -t rsa -C 'xxxxx@company.com' -f ~/.ssh/gitee_id_rsa
```

1. 生成一个github用的SSH-Key

```shell
$ ssh-keygen -t rsa -C 'xxxxx@qq.com' -f ~/.ssh/github_id_rsa
```

1. 在 ~/.ssh 目录下新建一个config文件，添加如下内容（其中Host和HostName填写git服务器的域名，IdentityFile指定私钥的路径）

```shell
# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitee_id_rsa
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_id_rsa
```

4.用ssh命令分别测试

```shell
$ ssh -T git@gitee.com
$ ssh -T git@github.com
```

这里以gitee为例，成功的话会返回下图内容

![输入图片说明](https://images.gitee.com/uploads/images/2018/0921/161137_b71ef6be_967230.png)



## git基础

通常有两种方式建立仓库

### 	1、在目录中初始化仓库

``` shell
 打开具体文件夹 执行 $ git init
 git init 文件夹内容 
 #
```

### 	2、clone远程仓库

``` shell
执行git clone -b '分支名称' 仓库地址

添加生成公钥：ssh-keygen -t rsa -C "xxxxx@xxxxx.com"  
```



## git 基本命令

### 1、撤销操作

``` shell
$ git commit --amend 

git commit -m 'initial commit'
git add forgotten_file
git commit --amend    
```

### 2 、取消暂存的文件

``` shell
git reset HEAD <file>//可以指定具体文件也可以不带 此时 代表取消全部
```

### 3、撤销对文件的修改

``` shell
git checkout --<file> 对文件的本地修改将会全部撤销   //是个危险的命令
```

### 4、远程仓库的使用

#### 	查看远程仓库

     ``` shell
### 后面再学习

git remote 
git remote -v  

     ```
    
     ```

#### 	添加远程仓库

 ```shell
git remote add <shortname> <url> #添加一个新的远程Git 仓库，同时指定一个方便使用的简写
eg：git remote add pb +地址

git fetch pb 可以拉去 pb 仓库中有，而自己仓库中没有的信息
 ```

#### 	从远程仓库中抓取与拉取

``` shell
git fetch <remote>  # 只会将数据下载到你的本地仓库 并不会自动合并或修改#
git pull # 会自动合并
```

####   	推送到远程分支

``` shell
git push origin master # 将分支推送到远程  如果远程不存在该分支，远程将会创建该分支
                       # 当有别人推送过 该分支，推送会被拒绝，需要从新拉去合并后才能推送 -f 强制合并
```

####  	查看某个远程分支

```she
git remote show origin 
```

#### 	远程仓库重命名和移除

```shell
git remote rename pb paul(origin)
git remote remove # 
```

####  打标签

```shel
git tag 
```

#### 多次commit 合并

```shell
git rebase -i HEAD~3  #最近三次提交合并
git push origin  分支名  -f # 强制推送到远程


回退多次合并
git reflog 
git reset --hard HEAD@{？}回到指定的head
```

#### git 删除分支和恢复

```shell
# 删除本地分支
git branch -d <branch_name>
# 删除远程分支
git push origin --delete <branch_name>
# 恢复本地分支
git reflog --date=iso 查看分支历史  有committ 就会有记录 获取 hash值
git branch <branch_name> <hash_val>
```

#### git 指定提交应用于其它分支

``` shell
git cherry-pick <commitHash>
git cherry-pick A^..B 【A到B包含A】 
```

#### git 回退版本到某个分支

```shell
$ git reset --hard HEAD^ 回退到上个版本
$ git reset --hard HEAD~3 回退到前3次提交之前，以此类推，回退到n次提交之前
$ git reset --hard commit_id 退到/进到 指定commit的sha码
强推到远程：
$ git push origin HEAD --force
```

#### git fetch 与 git pull 区别

```shell
git pull = git fetch + git merge，
```

![img](http://kmknkk.oss-cn-beijing.aliyuncs.com/image/git.jpg)



#### git 单个文件操作

```git
git log --pretty  文件名 //查看单个文件的修改历史
git reset commitid 文件名 //指定文件回退到指定版本


git checkout <sha1-of-a-commit> </path/to/your/file>  撤销单个文件到某次提交
$ git status -sb   查看修改显示
```

#### 切换远程分支

```shell 
git checkout -b  远程分支名称////release origin/release-9.4
```



npm run fix  修复问题

'meeting-schx:根据最近ui设计稿调整会议列表-会议详情中会议信息议题与资料显示样式'

*<!-- eslint-disable-next-line -->*  下行不检查eslint





  // eslint-disable-next-line

​    deptName: value.source ? (personInfo ? personInfo.deptName : '') : '外部人员',



