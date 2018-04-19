# wt-project
a project for wepy and git

# git练习记录
在本地创建版本库并推送到远程：



  $ git init
    在本地创建版本库：可以是空的文件夹，也可以是有内容的文件夹
    不管是空文件夹还是非空文件夹都会
    Initialized empty Git repository
    提示这是一个空的版本库

    空文件夹的话需要放入相应需要添加的文件

    $ git add .
    把文件添加到仓库

    $ git commit -m 'first commit'
    把文件提交到仓库

    至此，本地版本库建好了




  远程Create a new repository

    填入仓库名称和Description，其他保持默认配置

    $ git remote add origin git@github.com:wangtongbef/wt-project.git
    关联远程仓库

    $ git push -u origin master
    把当前分支master推送到远程
    -u 表示把本地的master分支和远程的master分支关联起来

    至此本地仓库顺利添加到远程并与master分支关联

分支管理练习

    $ git branch -vv
    显示本地分支与远程分支的对应关系

    $ git checkout -b dev
    创建并切换到新的dev分支 ：此时没有相对应的远程分支






