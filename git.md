# Git（分布式版本控制系统）

是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

# 特点

分布式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（git clone），在本地机器上拷贝一个完整的Git仓库。

## Git的功能特性：

### 从一般开发者的角度来看，git有以下功能：

- 1、从服务器上克隆完整的Git仓库（包括代码和版本信息）到单机上。
- 2、在自己的机器上根据不同的开发目的，创建分支，修改代码。
- 3、在单机上自己创建的分支上提交代码。
- 4、在单机上合并分支。
- 5、把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。
- 6、生成补丁（patch），把补丁发送给主开发者。
- 7、看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。
- 8、一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。

### 从主开发者的角度（假设主开发者不用开发代码）看，git有以下功能：

- 1、查看邮件或者通过其它方式查看一般开发者的提交状态。
- 2、打上补丁，解决冲突（可以自己解决，也可以要求开发者之间解决以后再重新提交，如果是开源项目，还要决定哪些补丁有用，哪些不用）。
- 3、向公共服务器提交结果，然后通知所有开发人员。

优点：

- 适合分布式开发，强调个体。
- 公共服务器压力和数据量都不会太大。
- 速度快、灵活。
- 任意两个开发者之间可以很容易的解决冲突。
- 离线工作。
   缺点：
- 资料少（起码中文资料很少）。
- 学习周期相对而言比较长。
- 不符合常规思维。
- 代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。



### Git的工作区、暂存区和版本库

* 工作区：就是你的电脑能够看到的目录
* 暂存区：一般存放在`.git`目录下的`index`文件中，所以我们有时也把暂存区叫做索引（index）
* 版本库：工作区有一个隐藏的`.git`，这个不算是工作区，而是git的版本库



### Git常用命令速查表

![](/Users/quinlan/Desktop/王培申的demo文件/git.png)

1、从git 官网下载程序，默认安装即可。

　　2、设置账号和邮箱关联，账号和邮箱可以是码云、GitLab...的账号都行：

```
$ git config --global user.name "Your Name"             
$ git config --global user.email "email@example.com"
```

　　3、选择合适地方，创建空目录：

```
$ mkdir test        //创建空目录，目录名字为test
$ cd test   　　　　 //进入test目录
```

　　4、初始化仓库，把目录变成git 可以管理的仓库：

```
$ git init
$ ls         //查看文件
$ ls -ah       //如果.git目录是影藏的话，可以通过这个命令查看.git目录
```

　　5、提交文件到git 上

```
$ git add .     　　　　　　　　　　　　 //告诉Git，把文件添加到仓库，此时是将修改添加到暂存区，可add 多次
$ git commit -m '本次提交的备注'       //告诉Git把文件提交到仓库，此时是吧暂存区的所有内容提交到当前分支，可一次提交很多文件
```

　　6、查看当前仓库的状态

```
$ git status    //查看版本库状态，什么被修改过但还没提交的

$ git diff      //查看当前相对上一次提交修改的内容
```

　　7、版本回退

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ git log                         //显示从最近到最远的提交日志
$ git log   --pretty== oneline     //显示log,但是不显示很多凌乱的信息
q                                //显示log版本信息有很多，使用q键停止查看
git reset —hard head^         //回退到上一个版本
git reset —hard head^^        //回退到上上个版本
git reset —hard head~100      //回退到之前100个版本
git reset —hard +commit_id    //回到某个版本号的版本

git reset — hard 版本号     //版本回退多次后需要恢复最新版本

$ git reflog                     //查看曾经使用过的命令
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　8、撤销修改

```
$ git checkout -- test.html
```

　　9、删除文件

```
$ rm test.index     //可直接在文件管理中删除文件，要不用rm 命令去删除

$ git rm test.html    //从版本库中删除
$ git commit -m '删除 test.html文件'
$ git branch -D <name>     //丢弃一个没有被合并过的分支，可以通过强行删除。
```

**远程仓库** 

　　1、创建SSH Key(需要生成 id_rsa私钥 和 id_rsa.pub公钥 两个文件)

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

　　2、登录GitHub，设置"SSH Keys",复制 id_rsa.pub 内容去添加。可允许添加多个SSH。

　　3、关联远程仓库

```
$ git remote add origin git@github.com：账户名
```

　　4、将本地的内容推送到远程库分支上

```
$ git push -u origin 分支名字       //第一次推送分支所有内容
$ git push origin 分支名字          //推送最新修改
```

　　5、查看远程仓库信息

```
$ git remote 

$ git remote -v      //查看更加详细的信息
```

**克隆**

```
$ git clone 需要克隆的仓库地址
```

**创建分支，并且切换过去**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ git checkout -b 新分支的名字       //创建分支并且切入进分支

或者等同于

$ git branch 分支名       //创建分支
$ git checkout 分支名     //切换到分支
$ git branch               //查看分支
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**合并分支**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ git checkout -b dev
$ git branch
$ git add .
$ git commit -m '提交test文件到dev分支'
$ git checkout master     //切换到主分支
$ git merge dev        //将dev分支上的内容合并到master分支上，合并 指定分支 到 当前分支
$ git merge --no-ff -m "merge with no-ff" dev  //合并分支时加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，通过git log查看
$ git branch -d dev     //删除dev分支
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

**解决冲突：**

　　同一文件修改冲突，需要手动解决冲突后再提交。git status可查看冲突，根据标记可修改冲突部分，修改结束后再重新提交。

```
$ git pull         //拉取远程内容
$ git log --graph        //命令可以看到分支合并图。
```

 **关联本地仓库和远程仓库**

```
$ git branch --set-upstream-to <branch-name> origin/<branch-name>
```

**创建标签**

```
$ git branch 
$ git checkout dev
$ git tag v1.0      //为当前需要打标签的分支打新标签

$ git tag        //查看所有标签
$ git tag -a 指定标签信息 -m "blablabla..."   //可指定标签信息 
```

**操作标签** 

```
$ git push origin <tagname>     //可以推送一个本地标签；
$ git push origin --tags        //可以推送全部未推送过的本地标签；
$ git tag -d <tagname>        //可以删除一个本地标签；
$ git push origin :refs/tags/<tagname>     //可以删除一个远程标签。
```