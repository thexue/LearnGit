## 安装与配置
[教程链接](https://blog.csdn.net/lzw_Z1902/article/details/128216848)
## 代码上传到远程仓库
![在这里插入图片描述](https://img-blog.csdnimg.cn/a9077bd504684cfb92b351db4453006e.png)
workspace：当前所在的工作目录
stagingarea：修改暂存区
loacl repository：本地仓库
remote respository ：远程仓库
我们首先在workspace目录编写代码、修改文件，然后需要使用add方法先将修改的部分添加到暂存区，commit方法添加到本地仓库。最终使用push方法上传代码。

```bash
总流程：
git init //将当前目录初始化为git可管理目录，生成.git目录里面包含文件相关信息
git add .//将当前目录下的所有修改文件提交至暂存区
git commit -m "first commit"//将暂存区的内容添加至本地仓库，并注释“first commit”
git remote add origin https://github.com/liyinchigithub/Git-commands.git//绑定所需要的远程仓库
git push origin master//提交代码到master分支
```


```bash
git add:
git add Test//添加指定目录到暂存区，包括子目录：
git add README hello.js //添加2个文件到暂存区
git add .//添加当前目录下的所有文件到暂存区：
```

```bash
git commit:
git commit -m "提交内容备注"
```

```bash
git push:
git push origin master//将本地的 master 分支推送到 origin 主机的 master 分支。
git push --force origin master//本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数：
git push <远程主机名> <本地分支名>:<远程分支名>
```

```bash
remote：
git remote add origin https://github.com/liyinchigithub/Git-commands.git//绑定相关远程库
```

## 分支
创建一个分支相当于新建一个工作节点，不会影响其它已有代码看，如图新建了一个new分支
![在这里插入图片描述](https://img-blog.csdnimg.cn/c72bf21983fd4cd7baacb1fe68b1c27c.png)

```bash
branch：
git branch //查看当前所有分支
git branch new//创建一个新分支new
git checkout new//切换到 new
git branch -d new//删除new分支
git push origin --delete new//删除远程代码库的new分支
```

## 分支合并
假设两个人同时在一个项目上面编写代码，A进行base分支，B进行new分支，他们都进行了一下代码更改，项目进展如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/cb79f1922a0b43639c43053dcb7132ac.png)

如果将new添加到base上即为图1，将base添加到new中如图2
![在这里插入图片描述](https://img-blog.csdnimg.cn/df6ff917efd74a36b65a389a71e4c31f.png)


合并原理为三项合并，假设当前是将new合并至base中
![在这里插入图片描述](https://img-blog.csdnimg.cn/002e931b3f9244e9bced04ebd9968eae.png)
这个base 为他们最近公共祖先，Mine为当前base，Yours为now分支合并后代码为

```
Paint（”hello“）;(蓝色节点)
```
这个样子就是发生冲突了，是无法合并的，需要修改
![在这里插入图片描述](https://img-blog.csdnimg.cn/043ad0029e9843dba5b8ecccedd5e3c1.png)

```bash
git checkout new//切换到new工作节点
git pull//拉取相关代码并进行编码
git checkout master//切换为主分支
git merge new//将new分支合并到master分支
git push -u origin master//推送至远程库
```


## 回滚

```bash
git log // 查询要回滚的 commit_id
 
git reset --hard commit_id // HEAD 就会指向此次的提交记录
 
git push origin HEAD --force // 强制推送到远端
```

```bash
git reset HEAD^ hello.js //回退hello.js的上个版本
git reset --hard origin/master//回退成线上版本
```
## 撤销提交

```bash
git log // 查找需要撤销的 commit_id
 
git revert commit_id  // 撤销这次提交
```
## 日志

```bash
git log --author//查看指定作者
git log --reverse //翻转
git log --oneline --before={3.weeks.ago} --after={2020-04-23} --no-merges//查看指定日期
git log --graph//查看分支合并情况
```
## 删除修改文件

```bash
git rm <file> // 从工作区和暂存区删除某个文件
 
git commit -m "" // 再次提交到仓库
git checkout -- <file>//暂存区覆盖工作区
git rm --cached <file>//工作区不做改变
```
## 从远程仓库拉取代码

```bash
git pull origin
git pull https://github.com/liyinchigithub/Git-commands.git
```
## 对比暂存区和工作区

```bash
git status
```
##  标签
版本可能会有多次提交，我们可以把某个提交打上标签，作为一个里程碑（version）

```bash
git add .
 
git commit -m "first commit"
 
git push origin master
 
git push origin v1.0
```

```bash
git push origin :refs/tags/v1.0//删除分支
```