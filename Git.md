# Git

## 版本控制（Revision control）

在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，

备份以便恢复以前版本的软件工程技术。

- 实现跨区域多人协同开发
- 追踪或记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发，提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间，同时降低人为错误

管理多人协同开发项目的技术



常见的版本控制工具

- Git
- SVN（Subversion）
- CVS（Concurrent ）
- VSS（Microsoft Visual SourceSafe）
- TFS（Team Foundation Server）
- Visual Studio Online

## 版本控制分类

### 1. 本地版本控制

记录文件每次的更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人用。

![本地版本控制](/Users/liuyu/Desktop/Android-Study/screenshots/本地版本控制.png)

### 2. 集中版本控制 代表SVN

所有的版本数据都保存在服务器上，协同开发者从服务器上同步更新或上传自己的修改。

所有的版本数据都存在服务器上，用户的本地只有自己以前所同步的版本，如果不联网的话，用户就看不到历史版本，也无法切换版本验证问题，或在不同分支工作。而且，所有数据都保存在单一的服务器上，有很大风险这个服务器会损坏，这样就会丢失所有的数据，当然可以定期备份。

![集中版本控制](/Users/liuyu/Desktop/Android-Study/screenshots/集中版本控制.png)

### 3. 分布式版本控制

所有的版本信息全部同步到本地的每个用户，可以在本地查看所有版本历史，也可以离线本地提交。只需要在联网时push到相应的服务器或其他用户那里。由于每个用户那里保存的都是所有的版本数据，只要有一个用户的设备没有问题就可以恢复所有的数据，但这增加了本地存储空间的占用。



不会因为服务器损坏或者网络问题，造成不能工作的情况。

![分布式版本控制](/Users/liuyu/Desktop/Android-Study/screenshots/分布式版本控制.png)



### Git与SVN最主要的区别

- SVN是集中式版本控制系统，版本库是集中放在中央服务器的，工作的时候用自己的电脑，所以首先要从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。集中式版本控制是必须联网才能工作，对网络带宽要求较高。
- Git是分布式版本控制系统，没有中央服务器。每个人电脑就是一个完整的版本库，工作的时候不需要联网，因为版本都在自己电脑上。协同的方法是这样的：比如自己电脑上改了文件A，其他人也在电脑上改了文件A，这时，只需要把各自的修改推送给对方，就可以互相看到对方的修改了。

Git是目前世界上最先进的分布式版本控制系统。



## Git 环境配置



## 基本Linux命令

| 命令    |                                                              |
| ------- | ------------------------------------------------------------ |
| cd      | 改变目录                                                     |
| cd..    | 回退到上一个目录，直接cd进入默认目录                         |
| pwd     | 显示当前所在的目录路径                                       |
| ls (ll) | 列出当前目录中的所有文件，只不过 ll 列出的内容更详细         |
| touch   | 新建一个文件 如touch index.js就会在当前目录下新建一个index.js文件 |
| rm      | 删除一个文件，rm index.js 就回把index.js文件删除             |
| mkdir   | 新建一个目录，就是新建一个文件夹                             |
| rm -r   | 删除一个文件夹，rm -r src删除src目录                         |
| mv      | 移动文件，mv index.html src。 index.html 是要移动的文件，src是目标文件夹，当然，这样写，必须保证文件和目标文件夹在同一个目录下。 |
| reset   | 重新初始化终端/清屏                                          |
| clear   | 清屏                                                         |
| history | 查看命令历史                                                 |
| help    | 帮助                                                         |
| exit    | 退出                                                         |
| #       | 注释                                                         |



## Git 基本理论（核心）

Git本地有三个工作区域：工作目录（Working Directory）、暂存区（Stage / Index）、资源库（Repository或Git Directory）。如果在加上远程的git仓库（Remote Directory）就可以分成四个工作区域。文件在这四个区域之间的转换关系如下：

<img src="/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-06-02 11.02.08.png" align=left></img>

**Workingspace**：工作区，平时存放代码的地方。

**Index / Stage**：暂存区，用于临时存放改动，只是一个文件，保存即将提交的文件列表信息。

**Repository**：仓库区（即本地仓库），安全存放数据的位置，里面有提交的所有版本的数据。其中HEAD指向最新放入仓库的版本。

**Remote**：远程仓库，托管代码的服务器，可以简单的认为是项目组中的一台电脑用于远程数据交换。



本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

<img src="/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-06-02 13.05.33.png" align=left></img>



## Git的基本工作流程

1. 在工作目录添加、修改文件
2. 将需要进行版本管理的文件放入暂存区域。git add .
3. 将暂存区域的文件提交到git仓库。               git commit
4. （如果需要远程仓库）。                               git push

**因此**，git管理的文件有三种状态：已修改（modified），已暂存（staged），已提交（committed）



## Git 项目搭建

工作目录（Workspace）一般就是希望Git帮助管理的文件夹，可以是项目的目录，也可以是一个空目录，建议不要有中文。

日常使用只要记住下图6个命令：

![git常用命令](/Users/liuyu/Desktop/Android-Study/screenshots/git常用命令.png)



### 创建本地仓库的方法

#### 1. 创建全新仓库

在需要git管理的根目录执行：

```bash
# 在当前目录新建一个Git代码库
$ git init
```

执行后可以看到，仅仅在项目目录多出了一个 .git目录，关于版本等所有信息都在这个目录里。

#### 2. 克隆远程仓库

将远程服务器上的仓库完全镜像一份至本地

```bash
# 克隆一个项目和它的整个代码历史（版本信息）
$ git clone [url]
```



## Git 文件操作

版本控制就是对文件的版本控制，对文件进行修改、提交等操作，需要先知道文件当前在什么状态。

- **Untracked：** 未跟踪，未加入到git库，不参与版本控制。通过 <mark>git add</mark> 状态变为 <mark>staged</mark>。
- **Unmodify：** 文件已经入库，未修改。即版本库中的文件快照内容与文件夹中完全一致，这种类型的文件有两种去处，如果它被修改，变为 <mark>Modified</mark>。如果使用<mark> git rm </mark>移出版本库，则成为<mark> untracked </mark>文件。
- **Modified：** 文件已修改，仅仅是修改， 并没有进行其他的操作，这个文件也有两个去处，通过<mark> git add </mark>可进入暂存<mark>staged </mark>状态，使用<mark> git check </mark>则丢弃修改过，返回到<mark> unmodify </mark> 状态，这个<mark> git ckeckout </mark> 即从库中取出文件，覆盖当前修改！
- **Staged：** 暂存状态，执行<mark> git commit </mark>则将修改同步到库中，这是库中的文件和本地文件又变为一致的内容，文件为<mark> unmodify </mark>状态。执行<mark> git reset HEAD filename </mark>取消暂存，文件状态为<mark> Modified</mark>。



实操：

```bash
# 初始化 Git
$ git init

# 查看文件状态
$ git status
```

<img src="/Users/liuyu/Desktop/Android-Study/screenshots/git init & status.png" alt="git init & status" style="zoom: 50%;" align="left"/>

```bash
# 添加所有文件到暂存区
$ git add .
$ git status

# 提交暂存区中的内容到本地仓库 -m 提交信息
$ git commit -m
```

使用<mark>git add .</mark>之后暂存区内，有文件了。

<img src="/Users/liuyu/Desktop/Android-Study/screenshots/git add. $ status.png" alt="git add. $ status" style="zoom: 50%;" align="left"/>

## 忽略文件

在现在的idea或android studio中使用git命令时，会自动生成一个[.gitignore]文件，可以在文件中配置哪些文件不参与到git的版本控制中。

![忽略文件规则](/Users/liuyu/Desktop/Android-Study/screenshots/忽略文件规则.png)



## Git 理解

 ```bash
# 创建一个可以运行 git 的环境
git init
# 先看看项目里有哪些变动了
# 直接 add .就加了全部，先从 status 看有哪些，选择add
git status
# 添加到暂存区，
git add
# 再使用 commit 把更新提交到本地仓库
git commit -m
# 把 更新 推到远端仓库
git push origin master
 ```

<img src="/Users/liuyu/Desktop/Android-Study/screenshots/git操作流程.png" align="left"></img>



## 集成 Git





## 说明：Git分支

git分支中常用指令：

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 切换已存在分支
git checkout [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

多个分支如果并行执行，就会导致我们代码不冲突，也就是存在多个版本！

web-api        -A

web-admin  -B  B会调用A

web-app       -C  C会调用B 间接调用A

如果冲突了就需要协商

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留别人的代码还是自己的代码。

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

![git_merge](/Users/liuyu/Desktop/Android-Study/screenshots/git_merge.png)



for now this is test branch
