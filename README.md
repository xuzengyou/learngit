# wt-project
a project for wepy and git

# git练习记录
  在本地创建版本库并推送到远程：

  创建本地版本库

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
    关联远程仓库（空库可实现）

    如果本地库是空的那么可以关联远程库但是不可以推送分支

    $ git push -u origin master
    把当前分支master推送到远程（空库不可实现）
    -u 表示把本地的master分支和远程的master分支关联起来

    至此本地仓库顺利添加到远程并与master分支关联

  分支管理练习

    $ git branch -vv
    显示本地分支与远程分支的对应关系

    $ git checkout -b dev origin/dev
    有origin/dev时 在本地创建并切换到相应的dev分支 此时 dev与origin/dev 已经关联

    $ git checkout master
    切换到master分支
    $ git checkout -b dev
    创建并切换到新的dev分支 ：此时没有相对应的远程分支
    创建的分支指向当前分支最新的一步

    $ git push origin dev
    将本地该分支上的所有本地提交推送到远程库  并会添加一个dev远程库 dev与origin/dev 并没有关联

    $ git branch --set-upstream-to=origin/dev dev
    将本地dev与origin/dev相关联

    $ git merge dev
    将dev分支合并到当前分支
    此时只是本地版本库的变化，还需要git push一下

    $ git branch -d dev
    删除本地库中的dev分支
    $ git branch -D dev
    强制删除未合并的本地库的dev分支

    $ git remote
    查看远程库的信息

    $ git remote -v
    显示可以抓取和推送的origin的地址 如果没有推送权限 就看不到push的地址

    $ git branch -r -d origin/dev
    $ git push origin :dev
    两行代码合起来可以做删除远程分支的操作

  修改用户名与邮箱

    $ git config --global user.name 'wangtong'
    修改用户名

    $ git config --global user.email wangt173111@163.com
    修改邮箱

  版本回退

    $ git log
    查看版本详细历史，基准为commit
    $ git log --pretty=oneline
    查看版本简略历史，多条

    $ git reflog
    查看版本库变化命令历史多条

    $ git reset --hard 2f640ed
    指定回退到某一版本或某一命令
    $ git reset --hard HEAD^
    回退到上一个版本

  打tag(暂时没用，后续整理)

# wepy框架学习(基础，待补充)


  目录结构：

    ├── dist                   小程序运行代码目录（该目录由WePY的build指令自动编译生成，请不要直接修改该目录下的文件）
    ├── node_modules
    ├── src                    代码编写的目录（该目录为使用WePY后的开发目录）
    |   ├── components         WePY组件目录（组件不属于完整页面，仅供完整页面或其他组件引用）
    |   |   ├── com_a.wpy      可复用的WePY组件a
    |   |   └── com_b.wpy      可复用的WePY组件b
    |   ├── pages              WePY页面目录（属于完整页面）
    |   |   ├── index.wpy      index页面（经build后，会在dist目录下的pages目录生成index.js、index.json、index.wxml和index.wxss文件）
    |   |   └── other.wpy      other页面（经build后，会在dist目录下的pages目录生成other.js、other.json、other.wxml和other.wxss文件）
    |   └── app.wpy            小程序配置项（全局数据、样式、声明钩子等；经build后，会在dist目录下生成app.js、app.json和app.wxss文件）
    └── package.json           项目的package配置

  基本操作(类vue)

    npm install wepy-cli -g
    cnpm install wepy-cli -g
    全局安装或更新WePY命令行工具

    wepy list
    列出所有官方/第三方wepy模板资源

    wepy init wepyjs/wepy-wechat-demo test-project
    拉取相应的模板并根据模板搭建项目

    npm install
    cnpm install
    安装相应依赖

    wepy与wepy-cli不冲突，wepy-cli是wepy的一个命令行管理工具

    wepy -v
    查看wepy版本号

    wepy upgrade --wepy to the latest version
    wepy upgrade --cli to the latest version
    升级wepy-cli到最新版本

    wepy build --watch
    此时开启实时编译

    wepy build --no-cache
    重启编译 对于引用到的文件，即使无改动也会再次编译

  偏向细节

    在wepy中实现promise的使用(未引入，未验证)(Promise已引入，无法验证官方文档的正确性)
      npm install promise-polyfill --save
      安装promise-polyfill以使项目能够使用promise

      在app.wpy中引入polyfill
      import Promise from 'promise-polyfill';

      在app.wpy中使API promise化
      export default class extends wepy.app {
        constructor () {
          super();
          this.use('promisify');
        }
      }
