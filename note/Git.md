## Git 设置

### 1. 设置全局用户名和邮箱

```java
git config --global user.name "Your Name"
git config --global user.email "youremail@xxx"
```

### 2. 添加  Key - Add public key

- Add your public key
  Note: [Here](https://help.github.com/enterprise/2.15/user/articles/connecting-to-github-with-ssh) is the document about how to add the ssh key.

## Git 删除

### 1. 删除项目的 git 信息

进入项目根目录，打开 git 客户端，执行如下命令

```java
rm -rf .git
```

## Git 提交

### 1.  Git  通用提交流程

```java
Git add .
Git commit
Git fetch
Git rebase

如果有冲突，就解决冲突然后执行如下操作：
git add .
git rebase --continue 
如果没有冲突直接 git push
```

### 2. 提交  Git  项目到新的  Git  地址（推荐两种方式）

```java
1. 修改命令 
git remote set-url origin [url] 
例如：Git remote set-url origin gitlab@gitlab.chumob.com:PHP/hasoffer.git
2. 先删后加
git remote rm origin 
git remote add origin [url]
```

### 3. Git Commit 信息提交格式

Commit message 格式，注意冒号后面有空格

```java
# <type>: <subject>

# <body>
# 1. 说明代码变更的动机，为什么要这么做
# 2. 说明我是怎么做的，这么做有什么副作用

# <footer>

# 1. Summary
#    每次提交，Commit message 都包括三个部分：Header，Body 和 Footer
#    其中，Header 是必需的，Body 和 Footer 可以省略
#    不管是哪一个部分，任何一行都不得超过72个字符
# 2. Header
#    Header部分只有一行，包括两个字段：type（必需）和 subject（必需）
# 2.1. type
#    feat: 新功能（feature）
#    fix: 修补 bug
#    docs: 文档（documentation）
#    style: 格式（不影响代码运行的变动）
#    refactor: 重构（即不是新增功能，也不是修改 bug 的代码变动）
#    test: 增加测试
#    chore: 构建过程或辅助工具的变动
#    如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中
# 2.2. subject
#    应当简明扼要，它最好不超过 50 个字符，首字母大写，
#    使用现在时祈使语气，不要以句号结尾, 因为它相当于标题
# 3. Body
#    对本次 commit 的详细描述，可以分成多行
# 4. Footer
#    关闭 Issue 或者对不兼容变更的描述
# 5. Revert
#    如果当前 commit 用于撤销以前的 commit，则必须以revert: 开头，后面跟着被撤销 Commit 的 Header
#    Body 部分的格式是固定的，必须写成 This reverts commit <hash>，
#    其中的 hash 是被撤销 commit 的 SHA 标识符
# 参考：http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html
```

### 4. 修改已经 commit 的注释内容

```java
两种情况：
1. 已经将代码push到远程仓库
2. 还没将代码push到远程仓库，还在本地的仓库中

代码还在本地 -- 修改最后一次注释：（参考 https://www.jianshu.com/p/098d85a58bf1）

1. git commit --amend
2. 出现有注释的界面（你的注释应该显示在第一行）， 输入i进入修改模式，进行编辑修改
3. 修改好注释后，按 Esc键 退出编辑模式，输入:wq 保存并退出，此时已经修改完成
4. 修改完成后，输入 git rebase --continue

代码已经 push 到远程仓库（参考 https://www.jianshu.com/p/098d85a58bf1）
```

### 5. commit 调用模板描述本次提交内容

```javascript
如果描述没有固定的要求，就可以使用简单描述
git commit -m "描述"
```

```javascript
如果对每次提交的描述有严格的要求，则可以调用模板来完成 commit
    
1、在固定路径编辑好模板格式，例如：commit.txt
2、配置参数
设置模板路径
git config --global commit.template ~/work/commit.txt
设置commit编辑工具
git config --global core.editor vim
设置用户名
git config --global user.name "name"
设置用户邮箱
git config --global user.email "Email"

3、上传代码
更新代码
git add ***
git commit
git push
```



## Git 分支

### 1. 开辟新分支

```java
eg：开辟分支 issue-10
1.创建分支 git checkout -b issue-10 origin/master
2.更改代码
3.git add .
4.git commit
--5. git fetch（第一次不用调用）
--6. git rebase origin/issue-10（第一次不用调用）
7.git push origin issue-10:issue-10
```

### 2. 合并分支

```java
eg：将分支 issue-10 合并到分支 origin/master 上面:
1.检出 issue-10 到本地 git checkout issue-10
2.将 issue-10 rebase 到 origin/master     git rebase origin/master
3.有冲突，解决冲突，然后提交 git add .
4.继续 rebase git rebase --continue
5.最后切换到 master 分支，将 issue-10 merge 到 master 分支，执行 merge 操作 git merge issue-10
至此，issue-10 会 merge 到分支 master 上，issue-10 可删除。
```

### 3.  修改分支名称

<https://www.jianshu.com/p/cc740394faf5>

### 4.  提交本地代码到新分支

<https://blog.csdn.net/a19891024/article/details/54138029>

## Git 仓库

### 1.  克隆远程仓库

```java
git clone 仓库地址
cd qiniu-log-helper
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

### 2.  将本地项目绑定远程仓库

```java
cd existing_folder
git init
git remote add origin 仓库地址
git add .
git commit -m "Initial commit"
执行此步骤后，如果远程仓库有文件不在本地，直接执行 git push -u origin master
会报错，此时因为新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并以下：
git pull --rebase origin master
--等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了
git push -u origin master
    
参考链接：
https://www.cnblogs.com/smfx1314/p/8426115.html
```

## Git Tag

### 1. 打  tag  步骤

```java
1. master修改完毕后（包括 changelog.md 文档的变更），在网页上创建merge request，记住是从master到production。
2. 切换到 production 分支，执行 git merge master 命令。
3. 再执行 git push 命令。
4. 执行了 merge 和 push 命令后，查看网页端 merge 状态是否变更为 merged
5. 如果已经变更，在 production 分支打包
6. 在网页端打tag，引用在第五步打好的包。
7. 在 production 分支 fetch/rebase ，拉取刚刚打的 tag 信息。
```

## Git 收藏

### 1. 常用 git 命令收藏

<image src="https://github.com/hgncxzy/AndroidNote/raw/master/images/Git常用命令速查表.jpg?raw=true" width="850px"/>

### Git 教程

- [廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Git 飞行规则](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md)

 

 

 
