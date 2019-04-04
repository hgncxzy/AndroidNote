

### 提交

#### git 提交流程

Git add

Git commit

Git fetch

Git rebase

如果有冲突，就解决冲突然后git add git rebase --continue 

如果没有冲突直接git push

 

 ### 分支

#### 开辟分支

开辟分支issue-10

1.创建分支 git checkout -b issue-10 origin/master

2.更改代码

3.git add .

4.git commit

--5. git fetch（第一次不用调用）

--6. git rebase origin/issue-10（第一次不用调用）

7.git push origin issue-10:issue-10

#### 合并分支

将分支 issue-10 合并到分支 origin/master 上面:

1.检出 issue-10 到本地 git checkout issue-10

2.将 issue-10 rebase 到 origin/master     git rebase origin/master

3.有冲突，解决冲突，然后提交 git add .

4.继续 rebase git rebase --continue

5.最后切换到 master 分支，将 issue-10 merge 到 master 分支，执行 merge 操作 git merge issue-10

至此，issue-10 会 merge 到分支 master 上，issue-10 可删除。

#### git 修改分支名称

<https://www.jianshu.com/p/cc740394faf5>

### **git 提交本地代码到新分支**

<https://blog.csdn.net/a19891024/article/details/54138029>

 

### 设置



#### 全局设置

Git global setup

git config --global user.name "xzy"

git config --global user.email "xuzhuyun@qq.com"

 

### 仓库

#### 创建仓库

#### **1.克隆远程仓库**

git clone git@git.fcbox.com:IB/ITG/qiniu-log-helper.git

cd qiniu-log-helper

touch README.md

**git add README.md**

**git commit -m "add README"**

**git push -u origin master**

 

#### **2.将本地项目绑定远程仓库**

cd existing_folder

**git init**

**git remote add origin git@git.fcbox.com:IB/ITG/qiniu-log-helper.git**

**git add .**

**git commit -m "Initial commit"**

--新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并以下：

**git pull --rebase origin master**


--等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了

**git push -u origin master**

参考链接：
https://www.cnblogs.com/smfx1314/p/8426115.html
 

### Tag

### **打  tag  步骤**

1. master修改完毕后，在网页上创建merge request，记住是从master到production。

2. merge后，将production拉取到本地分支，然后打包，打tag(打 tag 在网页端操作)

 

 

 

 
