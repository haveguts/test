##git使用

Git是目前世界上最先进的分布式版本控制系统

很多人都知道，Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。

Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了，于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。


---

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

---


###代码仓库


* ####检出仓库:

  
  进入到你仓库文件夹下面
  
  ```
  git clone https://github.com/haveguts/learnGit.git
  ```
  
  访问远程仓库：
  
  HTTPS：读写仓库加密通道，有单次上传限制。
  
  SSH：读写仓库加密通道，无单次上传限制，需先在个人设置页面上传 SSH-RSA 公钥，完成配对验证。
  
  
  
* ####添加一个新的远程仓库

  ```
  git remote add learngit https://github.com/haveguts/learnGit.git
  ```
  
  
  用 git remote 命令来查看当前添加的远程仓库：
  
  ```
  git remote -v
  ```
  
  
  用字符串 learngit 指代对应的仓库地址了。比如说，要抓取所有 learngit 有的，但本地仓库没有的信息，可以运行:
  ```
  git fetch learngit
  ```
  
  
  也可以直接通过 git clone 命令来直接复制远程仓库到本地目录：
  
  ```
  git clone https://github.com/haveguts/learnGit.git
  ```
  
  自己定义新建文件夹的名称，可以在上面的命令末尾指定新的名字：
  
  ```
  git clone https://github.com/haveguts/learnGit.git chinegit
  ```

  
  查看当前工作目录下的文件状态
  
  ```
  git status
  ```
  
  跟踪新文件 
  
   ```
  git add
  ```
  
 只要在 “Changes to be committed” 这行下面的，就说明是已暂存状态。如果此时提交，那么该文件此时此刻的版本将被留存在历史记录中。
 
 在 git add 后面可以指明要跟踪的文件或目录路径。如果是目录的话，就说明要递归跟踪该目录下的所有文件。
 
 也可使用 
 ```
 git add .
 ```
 跟踪当前文件夹下所有文件
 
 
 
 现在的暂存区域已经准备妥当可以提交了。在此之前，请一定要确认还有什么修改过的或新建的文件还没有 git add 过，否则提交的时候不会记录这些还没暂存起来的变化。所以，每次准备提交前，最好先用 
 ```git status``` 看下，是不是都已暂存起来了，然后再运行提交命令 ```git commit``` 来完成提交。
 
 
 你可以直接输入 ```git commit``` 命令进行提交，这种方式会启动文本编辑器以便输入本次提交的说明

 默认会启用 shell 的环境变量 $EDITOR 所指定的编辑器，一般都是 vi 或 emacs，也可以通过 git config 命令来修改默认的编辑器。 以 ‘#’ 开头的行都被视为注释，在提交时将被丢弃。如果没有输入提交信息就推出编辑器，将放弃这次提交。


----
* ####把本地仓库推送到远程仓库:
	在github新建一个空仓库

	进入本地仓库目录下运行
```
git remote add origin https://github.com/haveguts/lichentest.git
```

	若本地已有readme文件，则直接运行：```git push -u origin master```

	若无readme文件 运行 ``` git pull --rebase origin master ``` 再运行 ```git push -u origin master```推送到远程仓库

---



* ####远程仓库

	```
	git push [远程仓库名] [分支名]
	
	```	
如果要把本地的 master 分支推送到 origin 服务器上，可以运行下面的命令：
```
Username for 'https://github.com': chinelee
```

	出现
```
The requested URL returned error: 403
```

	解决方案：
	
	```
	1.vim .gi/config

	2.修改 url = https://github.com/haveguts/learnGit.git 
		  url = https://chinelee@github.com/haveguts/learnGit.git
	```


###分支管理

* ####创建分支,并切换到新分支
 Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！
 

	```git checkout -b lichen```

	```git checkout```命令加上```-b```参数表示创建并切换，相当于以下两条命令：

	```
	git branch dev

	git checkout dev
	```

	对readme.txt做个修改，加上一行：

	```Creating a new branch is quick.```

	跟踪文件
	```
	git add readme.txt 
	```

	提交更改
	```
	git commit -m "lichen test"
	```
	
	切换回master分支

	```
	git checkout master
	```
	
	再查看一个readme.txt文件，刚才添加的内容不见了
	
	我们把刚才的分支工作成果合并到master分支上：
	```
	git merge lichen
	```
	
---
* ####分支常用命令

	```
	查看分支：git branch
	
	创建分支：git branch <name>
	
	切换分支：git checkout <name>
	
	创建+切换分支：git checkout -b <name>
	
	合并某分支到当前分支：git merge <name>
	
	删除分支：git branch -d <name>
	```

* ####分支冲突

	```
	创建新的分支
	git checkout -b lichen
	
	修改readme 文件
	提交
	git add readme.txt 
	git commit -m ""
	
	切换到master
	git checkout master
	
	修改readme
	然后提交
	git add readme.txt 
	git commit -m ""
	
	合并分支git merge lichen
	
	查看冲突并解决
	再提交
	git add readme.txt 
	git commit -m "conflict fixed"
	```

---
* ####提示：

	*master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。*

---

* ####多人合作:

	当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin
	
	要查看远程库的信息，用```git remote```
	
	推送分支
	
	推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
	
	```
	git push origin master
	```
	
	如果要推送其他分支，比如lichen，就改成：
	
	```
	git push origin lichen
	```
	
	
	
	*分支完全可以在本地自己藏着玩，是否推送，视你的心情而定*
	
	
	多人协作的工作模式通常是这样：
	
	首先，可以试图用```git push origin branch-name```推送自己的修改；
	
	如果推送失败，则因为远程分支比你的本地更新，需要先用```git pull```试图合并；

	如果合并有冲突，则解决冲突，并在本地提交；
	
	没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
	
	如果```git pull```提示```no tracking information```，则说明本地分支和远程分支的链接关系没有创建，用命令
	
	```git branch --set-upstream branch-name origin/branch-name```。
	
	在本地创建和远程分支对应的分支，使用
	
	```git checkout -b branch-name origin/branch-name```
	本地和远程分支的名称最好一致
	
	
	
	建立本地分支和远程分支的关联
	
	```	git branch --set-upstream branch-name origin/branch-name```
	

* ####标签管理

	在Git中打标签非常简单，首先，切换到需要打标签的分支上：
	```git checkout lichen```
	
	然后
	```git tag v1.0```
	
	``git tag `` 显示已有标签
	
	默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
	
	方法是找到历史提交的commit id，然后打上就可以了
	
	```
	git log --pretty=oneline --abbrev-commit
	
	git tag v0.9 9709c97
	```
	
	查看某个标签信息
	```
	git show v0.9
	```
	
	删除某个标签
	```
	git tag -d v0.9
	```
	
	因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
	
	如果要推送某个标签到远程，使用命令
	```
	git push origin <tagname>：
	```
	
	
	一次性推送全部尚未推送到远程的本地标签：
	```
	git push origin --tags
	```
	
	如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
	```
	git tag -d v0.9
	```
	
	再从远程删除
	
	```
	git push origin :refs/tags/v1.0
	```



* ####版本回退
	查看log
	```
	git log
	```
	
	```
	git reset --hard d4b9e11711d286bb
	```
	
	后悔了怎么办？
	```
	git reflog
	```

* ####删除文件 
删除文件 
```
git rm filename
```

	误删恢复
```git reset head lichen.py```

	```git checkout -- filename```




---
在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。



---

工作区（Working Directory）

版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。


Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支



###SSH
Windows下打开Git Bash
ssh-keygen -t rsa -C "youremail@example.com"

GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。