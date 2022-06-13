
### GIT版本控制系统
> 版本控制系统：

1.记录历史版本信息（记录每一次修改的记录）
2.方便团队相互之间协作开发
......
> 常用的版本控制系统
- cvs/svn：集中式版本控制系统，必须有一个中央总控的服务器（用来存储历史版本和代码信息）
  + 拉取中央服务器上的最新代码到本地
  + 跑一遍，没问题后，开始自己的工作
  + 完成自己的工作内容后，再拉取，如果有冲突，自己本地把冲突代码合并
  + 上传到中央
  - svn弊端
    + 需要联网才能回退或查看历史版本信息
    + 中央服务器毁坏了，一切OVER
    + 所有的上传和下载都是基于文件传输方式完成的，速度会慢
- git：分布式版本控制系统，每个开发者本地就是一个代码管理仓库
  + 无需联网也能记录和查看历史版本信息
  + 无需过多依赖中央仓库，每个人本地也有全部的信息
  + 向中央仓库传输内容依托的是文件流传输，速度比SVN快
### 1.GIT工作原理
- 工作区：我们能看到的，并且用来写代码的区域
- 暂存区：临时存储用的
- 历史区：生成历史版本
从工作区提交到暂存区，从暂存区提交到历史区，是把内容复制一份传过去的，本区域中依然存在这些信息（只有这样才能对比出哪些文件在某个区）
工作区-$ git add -A->暂存区-$ git commit -m''->历史区->$ git pull origin master->$git push origin master->中央仓库
历史区/暂存区-$git check->工作区
**1.GIT的全局配置**
> 第一次安装完成git后，我们全局环境下配置基本信息：我是谁？
```
$ git config -l // 查看配置信息
$ git config --global -l // 查看全局配置信息

配置全局信息：用户名和邮箱
$ git config --global user.name 'xxx'
$ git config --global user.email 'xxx@xx.xx'
```
**2.创建仓库完成版本控制**
> 创建本地git仓库
```
$ git inint
//=>会生成一个隐藏文件夹".git"（这个文件夹千万不要删除，因为暂存区和历史区还有一些其他的信息都在这里，删了就不是一个完整的git仓库）
```
> 在本地编写完成代码后（在工作区），把一些文件提交到暂存区
```
$ git add xxx 把某一个文件或者文件夹提交到暂存区
$ git add . 把当前仓库中所有最新修改的文件都提交到暂存区
$ git add -A
$ git status 查看当前文件的状态（红色代表在工作区，绿色代表在暂存区，看不见东西证明所有修改的信息都已经提交到历史区
```
> 把暂存区内容提交到历史区
```
$ git commit -m'描述信息：本次提交内容的一个描述'
查看历史版本信息（历史记录）
$ git log
$ git reflog 包含回滚的信息
```
### GIT和GIT-HUB
> GIT-HUB：https://www.github.com
一个网站（一个开源的源代码管理平台），用户注册后，开源在自己账号下创建仓库，用来管理项目的源代码（源代码是基于git传到仓库中）
> 我们熟知的插件、类库、框架等都在这个平台上有托管，我们可以下载观看和研究源码等
1.Settings用户设置
  + Profile 可以修改自己的用户信息
  + Account 可以修改用户名
  + Security 可以修改自己的密码
  ...
2.创建仓库
  new repository-> 填写信息 ->Create repository
    + public 公共仓库作为开源项目
    + privat 私有仓库作为内部团队协作管理的项目
  Settings
    + Delete this repository 删除仓库
    + Collaborators 设置协作开发的人员
  Code 可以查看历史版本信息和分支信息
3.把本地仓库信息提交到远程仓库
```
// 建立本地仓库的和远程仓库的链接
// 查看本地仓库和哪些远程仓库保存链接
$ git remote -v
// 让本地仓库和远程仓库新建一个链接 origin是随便起的一个链接名（可以改成自己想要的，只不过一般都用这个名字）
$ git remote add origin [GIT远程仓库地址]
// 删除关联信息
$ git remote rm origin
```
```
// 提交前最好先拉取
$ git pull origin master
// 把本地代码提交到远程仓库（需要输入github的用户名密码）
$ git push origin master
```
```
$ git clone [远程仓库git地址] [别名：可以不设置，默认是仓库名]
/*
 * 真实项目开发流程：
 *    1.组长或者负责人先创建中央仓库
 *    2.小组成员基于$ git clone 把远程仓库及默认的内容克隆到本地一份（clone解决了三件事：初始化一个本地仓库“git init”、和对应的远程仓库也保持了关联“git remote add”、把远程仓库默认内容拉取到本地“git pull”）
 *    3.每个组员写完自己的程序后，基于“git add/git commit”把自己修改的内容存放到历史区，然后通过“git pull/git push”把本地信息和远程仓库信息保持同步即可（可能涉及冲突的处理）
 */
```
### NPM
> node package mager：NODE模块管理工具，根据NPM我们可快速安装、卸载所需要的资源文件（例如：jQuery、vue、vue-router...）
> 去NODE官网：https://nodejs.org/zh-cn/ 下载NODE，安装NODE后，NPM也就跟着安装了
$ node -v
$ npm -v 出现版本号证明安装成功
####基于npm进行模块管理
> https://www.npmjs.com/ 基于npm是从npmjs.com平台下载安装
```
$ npm install xxx 把模块安装在当前项目中（node_modules)
$ npm install xxx -g 把模块安装在全局环境中
$ npm i xxx@1.0.0 安装指定版本号的模块
$ npm view xxx versions > xxx.version.json 查看某个模块的版本信息（输出到指定JSON文件中）
$ npm init -y 初始化当前项目的配置依赖清单（项目文件夹的名字中不能出现中文、大写字母和特殊符号）
  =>  创建成功后会在当前项目中生成package.json的清单文件
  dependencies:生产依赖模块（开发和项目部署的时候都需要）
  devDependencies:开发依赖模块（只有开发的时候需要）
  scripts:配置本地可执行命令的
$ npm i xxx --save 把模块保存在清单生产依赖中
$ npm i xxx --save-dev 把模块保存在清单开发依赖中
$ npm install 跑环境，安装清单安装所需的模块
$ npm root -g 查看全局安装模块的目录
$ npm uninstall xxx
$ npm uninstall xxx -g 卸载安装过的模块
```

windows操作系统：在某个文件夹下执行DOS命令
1.windows + r -> 输入cmd -> 磁盘符 -> cd xxx
2.在文件夹地址栏直接输入cmd即可
3.在文件夹中“shift + 鼠标右键” -> 在此处打开命令窗口

如果想查看当前目录中的文件内容：dir

一个新项目的开始：
1.创建项目文件夹
2.把他作为一个新的仓库进行代码管理（可以基于$git clone把远程仓库克隆下来即可）
3.初始化模块配置清单package.json：$npm init -y
4.按照需要的模块：$nom i xxx
5.正常开发
6.开发中：可能需要在本地配置命令去完成一些功能（例如LESS文件编译，此时需要配置npm可执行的命令）
```
"scripts": {
    "ts": "lessc css/index.less css/index.min.css -x",
    "xxx": "webpack"
},
```
需要编译的时候。执行$npm run ts
...
7.开发中我们需要基于git把文件进行管理：生成对应的历史版本
  提交到暂存区、历史区、远程仓库的时候，项目中很多文件是无需处理和提交的，例如：node_module、.idea...，不需要提交的，我们生成一个.gitgnore忽略文件
8.由于每次git提交的时候，我们都不去提交node_modules，所以团队协作开发中，我们每当拉下项目代码的时候，都需要跑环境：执行$npm install，按照项目中的package.json中的依赖项信息，把缺失的模块都安装一遍