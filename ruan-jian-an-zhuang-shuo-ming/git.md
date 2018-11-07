---
description: Git安装及配置试用
---

# Git

### 下载安装 <a id="git-xia-zai-di-zhi-httpsgithubproductionreleaseasset-2-e65bes-3-amazonawscom-23216272-081b-0800c8-c2-11-e8-9-f25-2-e5ceff-4-ec-71-xamzalgorithmaws-4-hmacsha-256-xamzcredentialakiaiwnjyax-4-csveh-53-a-2-f20181104-2-fuseast-1-2fs-3-2faws-4-requestxamzdate-20181104-t033158zxamzexpires-300-xamzsignaturea-5-eb-55-e7b-27-a879b-3-e42826d-5-e7389c-85-ec-318-fbbbd-949-ff-9-c67cf-12-b73ceb-6-bxamzsignedheadershostactorid-0-responsecontentdispositionattachment-3-b-20-filename-3-dgit-2-19-1-64bitexeresponsecontenttypeapplication-2-foctetstream"></a>

1.  双击安装,默认安装即可

###  设置个人信息

```text
$ git config --global user.name "你的姓名"
$ git config --global user.email "你的邮箱"
```

###  设置ssh key\(pull/push代码无需输入密码验证,除第一次\)

生成ssh key

```text
ssh-keygen -t rsa -C "你的邮箱"  //一直回车
```

复制密钥

```text
Mac ~/.ssh\id_rsa.pub
Win C:\Users\你的用户\.ssh\id_rsa.pub
```

![](../.gitbook/assets/image%20%2810%29.png)

###   登录GitLab设置SSH Key

![](../.gitbook/assets/image%20%2815%29.png)

###  Ieda 设置Git

 找到 File--&gt;Setting-&gt;Version Control--&gt;Git--&gt;Path to Git executable 选择你的 git.exe

![](../.gitbook/assets/image%20%287%29.png)

导入项目/选择git导入

![](../.gitbook/assets/image%20%2812%29.png)

 输入git地址，选择代码目录

![](../.gitbook/assets/image%20%2811%29.png)

提交

![](../.gitbook/assets/image%20%2816%29.png)

###  常用命令   

```text
git init //初始化本地git环境
git clone XXX//克隆一份代码到本地仓库
git pull //把远程库的代码更新到工作台
git pull --rebase origin master //强制把远程库的代码跟新到当前分支上面
git fetch //把远程库的代码更新到本地库
git add . //把本地的修改加到stage中
git commit -m 'comments here' //把stage中的修改提交到本地库
git push //把本地库的修改提交到远程库中
git branch -r/-a //查看远程分支/全部分支
git checkout master/branch //切换到某个分支
git checkout -b test //新建test分支
git checkout -d test //删除test分支
git merge master //假设当前在test分支上面，把master分支上的修改同步到test分支上
git merge tool //调用merge工具
git stash //把未完成的修改缓存到栈容器中
git stash list //查看所有的缓存
git stash pop //恢复本地分支到缓存状态
git blame someFile //查看某个文件的每一行的修改记录（）谁在什么时候修改的）
git status //查看当前分支有哪些修改
git log //查看当前分支上面的日志信息
git diff //查看当前没有add的内容
git diff --cache //查看已经add但是没有commit的内容
git diff HEAD //上面两个内容的合并
git reset --hard HEAD //撤销本地修改
echo $HOME //查看git config的HOME路径
export $HOME=/c/gitconfig //配置git config的HOME路径

```

