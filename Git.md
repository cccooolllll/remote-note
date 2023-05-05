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

### Git常用命令

<a href="#git add">`git add`</a>: 将文件添加到暂存区

`git status`: 查看在你上次提交之后是否有对文件进行再次修改

`git diff`: 比较文件在暂存区和工作区的差异

`git ls-files`: 查看暂存区的文件

`git cat-file -p`: 查看暂存区文件中的内容

`git commit`: 提交暂存区文件到本地仓库

`git rm`: 删除文件



#### <a id="git add">git add</a>

