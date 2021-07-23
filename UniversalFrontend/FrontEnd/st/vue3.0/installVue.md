
## Vue3.0的学习

```
首页node.js
以及一些环境变量的配置
npm cnpm yarn的选择
安装 vue/cli脚手架
仓库管理
拷贝项目 git clone <地址>
创建分支 git branch '分支名'
切换分支git checkout '分支名'
创建分支并切换分支 git checkout -b '分支名'
添加所有修改的文件到暂存 git add .
查看状态git status
提交到本地 git commit -m '本次提交的说明'
提交到远程时，如需拉取当前远程分支的代码使用git pull origin '分支名'
提交到远程git push origin '分支名'
```

## 脚手架的安装

```
3.0的脚手架 使用npm i -g @vue/cli 安装，通过vue -V查看版本号
安装之前如果有旧版本的脚手架的话，可以先卸载npm uninstall vue-cli -g
我们如果想要在3.0的脚手架上使用2.0的命令去创建项目的话，需要安装npm install -g @vue/cli-init