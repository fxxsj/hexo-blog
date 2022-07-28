---
title: Hexo博客多端同步问题
date: 2022-07-28 08:41:36
tags: hexo
categories: 学习
---
## 博客源文件同步

在博客根目录执行

    git init
    git remote add origin git@github.com:fxxsj/fxxsj.github.io.git  # 添加远程仓库 注意这里要添加你自己的仓库 fxxsj 换成你自己的用户名
    git checkout -b hexo            # 新建hexo分支并切换到hexo分支
    git add .              # 所有变化提交到暂存区
    git commit -m "解决同步问题"  # 提交文件
    git push origin hexo   # 推送hexo分支

这就成功了，github上已经有博客的源文件了。

推荐把hexo设置为默认分支。

## git submodule 实现第三方主题同步

因为之前是直接把第三方主题克隆到博客目录，有什么改动是无法推送到作者Git仓库的，这个时候需要把第三方主题的项目Fork到自己仓库，自己账号下生成一个同名的仓库，并对应一个url，我们应该git clone自己账号下仓库的url。

Fork第三方主题

执行如下操作。

    git submodule add git@github.com:fxxsj/hexo-theme-argon.git themes/argon

把自己仓库下面第三方主题添加到Git子模块。

`
注 : themes/argon 这里的目录是因为我用的argon主题才会写themes/argon 如果你用的不是argon,请把argon替换成你的第三方主题文件夹名字。
`

博客的根目录会多一个.gitmodules文件,这是一个配置文件，保存了项目 URL 和你拉取到的本地子目录。
.gitmodules文件

这就添加成功了，然后执行如下操作。

    git add .              # 所有变化提交到暂存区
    git commit -m "添加第三方主题Git子模块"  # 提交文件
    git push origin hexo   # 推送hexo分支

## 更换电脑同步博客和第三方主题

### 同步博客
电脑上一定要先node和git，执行如下操作。

    npm install hexo-cli -g  # 先安装hexo的脚手架
    git clone git@github.com:fxxsj/fxxsj.github.io.git  # 下载项目，因为hexo 是默认分支，所以这里直接会下载hexo分支
    npm i # 安装依赖
    hexo s # 启动服务器

剩下的就自行操作了。博客已经完成了同步。

注：每次写完文章部署网站后，记得再执行如下操作。

    git add .             # 所有变化提交到暂存区
    git commit -m "新增xxx文章"      # 提交文件
    git push origin hexo           # 推送hexo分支

### 同步第三方主题

在博客根目录执行如下操作。

    git submodule init    # 初始化本地配置文件
    git submodule update    # 拉取子模块

如果第三方主题有修改的，修改完成后在第三方主题目录执行。

    git add .             # 所有变化提交到暂存区
    git commit -m "修改主题xxxx"      # 提交文件
    git push origin master       # 推送master分支

这样就会把修改的主题推送到自己的仓库。

修改的主题推送到自己的仓库

这样就实现多端同步了。

## 版权声明

>本文转载自[lanpangzhi](https://segmentfault.com/a/1190000019459014)。
>
> 感谢原作者，以及开源世界。