# 安装

```shell
sudo apt install git

```

**工作区** --- `git add` ---> **缓存区** --- `git commit` --->**本地仓库**
工作区：.git所在目录
暂存区：.git/index
本地仓库：.git/objects

状态：

未跟踪：Untrack

未修改：Unmodified

已修改：Modified

已暂存：Staged

# 基础操作

```shell
git init #初始化
git config --local user.name "rainbow"
git config --global user.email "rainbow@163.com"
sudo git config --system core.editor "nano"
# –local：当前 Git 仓库.git/config 当前仓库有效，不影响其他 Git 仓库
# –global：全局范围的 Git 配置,用户主目录.gitconfig(通常是 ~/.gitconfig)所有 Git 仓库都有效
# –system：系统范围的 Git 配置/etc/gitconfig
git config --global user.name "John Doe"	#配置用户名
git config --global user.email johndoe@example.com	#配置邮箱
#查看当前仓库配置
git config --global --list
git config --local --list
git config --system --list
#查看状态
git status
git log
git log --oneline #简略信息
git ls-files #查看暂存区的文件

#提交操作
git add . #提交所有文件到暂存区
git commit -m '第一次提交' #从暂存区提交到仓库
#删除操作
git rm [文件] #删除暂存区的文件
git rm --cached #删除本地加暂存区文件
#回退版本
git reset HEAD~	#指上一个版本
git reset HEAD^ #指上一个版本
git reset HEAD^2 #指上两个版本
git reset --soft #工作区和暂存区不会清空
git reset --hard #工作区和暂存区会清空
git reset --mixed #工作区不会清空，暂存区会清空（不加参数默认是这个）
#拉取仓库到本地
git clone
```

查看差异

```shell
git diff #查看工作区和暂存区的差异
git diff --cached #查看暂存区和本地仓库的差异
git diff [提交ID] [提交ID] #查看两次提交的差异
```

忽略文件

```shell
touch .gitignore
#把要忽略的文件名添加到.gitignore里面，提交的时候就忽略
#忽略模板可以直接获取
https://github.com/github/gitignore
```

添加github

```shell
ssh-keygen -t rsa -b 4096 #生产ssh公私密钥
id_rsa #密钥，本地存储，自行保留
id_rsa.pub #公钥，上传到远程仓库
git remote -v #查看管理仓库
git push -u origin main:main #关联分支

```

