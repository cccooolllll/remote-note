git 有四个区域:

- 3个本地区域
  - 工作区(Workspace): 存放项目代码的地方。
  - 暂存区(Stage): 存放临时的改动, 事实上它只是一个文件, 保存即将提交的文件列表信息。
  - 资源库(Repository): 安全存放数据的位置, 这里面有提交到所有版本的数据。其中 HEAD 指向最新放入仓库的版本。
- 1个远程区域
  - 远程库(Remote): 托管代码的服务器。

### Git初始化

```git
$ git init
```

初始化成功后，会出现一个`.git`的隐藏文件夹，这个就是项目的git仓库。

### Git配置

#### git config

查看git配置命令

```
$ git config --list
```

或者也可以在`.git`文件夹里中的`config`文件中查看。

```
$ git config		  #仅对当前仓库
$ git config --global #作用于系统上的所有仓库
```

设置用户信息

```
$ git config --global user.name "UserName"		#设置用户名，去掉--global仅对当前仓库生效
$ git config --global user.email "Email"		#设置邮箱,去掉--global仅对当前仓库生效
```

配置SSH代理



### Git常用命令

<a href="#git add">`git add`</a>: 将文件添加到暂存区

<a href="#git status">`git status`</a>: 查看在你上次提交之后是否有对文件进行再次修改

<a href="git diff">`git diff`</a>: 比较文件在暂存区和工作区的差异

<a href="#git ls-files">`git ls-files`</a>: 查看暂存区的文件

<a href="#git cat-file -p">`git cat-file -p`</a>: 查看暂存区文件中的内容

<a href="#git commit">`git commit`</a>: 提交暂存区文件到本地仓库

<a href="#git rm">`git rm`</a>: 删除文件



#### <a id="git add">git add</a>

```
# 1. 添加单个文件到缓存区，文件必须包含扩展名
$ git add <file>    

# 2. 添加文件夹中所有内容到缓存区
$ git add .         
```

#### <a id="git status">git status</a>

查看自从上次提交过之后，是否对文件进行再次修改，并提示修改过的文件

```
$ git status	#查看状态

$ git status -s		#查看详细文件状态
此命令下：
A 表示新提交
M 表示提交过，并且本地又修改了
AM 表示有改动
?? 表示有未知的新添加文件

$ git commit -m "提交"	#再次提交
```

#### <a id="git diff">git diff</a>

比较文件的不同, 即比较文件在暂存区和工作区的差异

git diff 显示已经写入暂存区和已经被修改但尚未写入暂存区文件的区别

应用场景:

```
git diff		#尚未缓存的改动
git diff --cached		#查看已经缓存的改动
git diff HEAD		#查看缓存成功和未缓存的所有改动
git diff --stat		#显示摘要而非整个diff
```

#### <a id="git ls-files">git ls-files</a>

查看暂存区的文件

```
$ git ls-files
```

可选参数:

- -c: 默认
- -d: 显示删除的文件
- -m: 显示被修改过的文件
- -o: 显示没有被 git 跟踪过的文件
- -s: 显示 mode 以及对应的 Blog对象, 进而可以获取暂存区中对应文件的内容

#### <a id="git cat-file -p">git cat-file -p</a>

查看暂存区文件中的内容

```
$ git ls-files -s
100644 5849920a9afa621d7ec9519a16b24a2009d56a9b 0       README.md

$ git cat-file -p 5849	#可以看到是长字符串的前四位数或者更多
# remote-note
远程仓库笔记
```

#### <a id="git commit">git commit</a>

提交暂存区文件到本地仓库

```
$ git commit -m [message]
```

提交暂存区的指定文件到本地仓库

```
$ git commit [file1] [file2] ... -m [message]
```

#### <a id="git rm">git rm</a>

1、将文件从暂存区和工作区中删除

```
$ git rm README.md
```

2、将文件从暂存区和工作区中强制删除

```
# 可以加上 -f, 表示强制删除之前修改过而且 add 到暂存区的文件
$ git rm -f README.md
```

3、将文件从暂存区删除，在工作区保留

```
git rm --cached README.md
```

### 分支操作

```
# 查看分支
$ git branch -a 

# 基于当前分支创建一个新分支
$ git checkout -b feature/hotfix-001

# 基于指定分支创建一个新的分支
$ git checkout -b feature/hotfix-002 master

# 切换分支
$ git checkout master

# 删除分支
$ git branch -d feature/hotfix-001
```
