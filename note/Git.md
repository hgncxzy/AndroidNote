### 全局设置 - Git global setup

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@xxx"
```

### 添加 Key - Add public key

- Add your public key
  Note: [Here](https://help.github.com/enterprise/2.15/user/articles/connecting-to-github-with-ssh) is the document about how to add the ssh key.

####  **删除项目的 git 信息**

进入项目根目录，打开 git 客户端，执行如下命令

```bash
rm -rf .git
```

### 提交 - Git 通过提交流程

```bash
Git add .
Git commit
Git fetch
Git rebase

如果有冲突，就解决冲突然后执行如下操作：
git add .
git rebase --continue 
如果没有冲突直接 git push
```



### 提交 - 提交 Git 项目到新的 Git 地址（推荐两种方式）

```bash
1. 修改命令 
git remote set-url origin [url] 
例如：Git remote set-url origin gitlab@gitlab.chumob.com:PHP/hasoffer.git
2. 先删后加
git remote rm origin 
git remote add origin [url]
```

### 提交 - Git Commit 信息提交格式

Commit message 格式，注意冒号后面有空格

```html
<type>: <subject>
type
用于说明 commit 的类别，只允许使用下面 7 个标识，也可以自己在配置文件中更改或者扩展。
标准类型如下：
feat：新功能（feature）
fix：修补bug
docs：文档（documentation）
style： 格式方面的优化
refactor：重构
test：测试
chore：构建过程或辅助工具的变动
    
subject
subject是 commit 目的的简短描述，不能超过 50 个字符，且结尾不加英文句号。
```

参考文章  https://www.jianshu.com/p/8efa36c5dfd4 

 ### 分支 - 开辟分支

```bash
eg：开辟分支 issue-10
1.创建分支 git checkout -b issue-10 origin/master
2.更改代码
3.git add .
4.git commit
--5. git fetch（第一次不用调用）
--6. git rebase origin/issue-10（第一次不用调用）
7.git push origin issue-10:issue-10
```

### 分支 - 合并分支

```bash
eg：将分支 issue-10 合并到分支 origin/master 上面:
1.检出 issue-10 到本地 git checkout issue-10
2.将 issue-10 rebase 到 origin/master     git rebase origin/master
3.有冲突，解决冲突，然后提交 git add .
4.继续 rebase git rebase --continue
5.最后切换到 master 分支，将 issue-10 merge 到 master 分支，执行 merge 操作 git merge issue-10
至此，issue-10 会 merge 到分支 master 上，issue-10 可删除。
```

### 分支 - 修改分支名称

<https://www.jianshu.com/p/cc740394faf5>

### 分支 - 提交本地代码到新分支

<https://blog.csdn.net/a19891024/article/details/54138029>

### 仓库 - 克隆远程仓库

```bash
git clone 仓库地址
cd qiniu-log-helper
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

### 仓库- 将本地项目绑定远程仓库

```bash
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
```

参考链接：
https://www.cnblogs.com/smfx1314/p/8426115.html

### Tag - 打  tag  步骤

```bash
1. master修改完毕后（包括 changelog.md 文档的变更），在网页上创建merge request，记住是从master到production。
2. 切换到 production 分支，执行 git merge master 命令。
3. 再执行 git push 命令。
4. 执行了 merge 和 push 命令后，查看网页端 merge 状态是否变更为 merged
5. 如果已经变更，在 production 分支打包
6. 在网页端打tag，引用在第五步打好的包。
7. 在 production 分支 fetch/rebase ，拉取刚刚打的 tag 信息。
```

### 常用 git 命令收藏

<image src="https://github.com/hgncxzy/AndroidNote/blob/master/images/Git常用命令速查表.jpg?raw=true" width="850px"/>

### Git 教程

- [廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Git 飞行规则](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md)

 

 

 
