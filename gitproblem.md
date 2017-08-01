## 使用git注意的一些问题

- 直接在命令行输入`git`得到帮助说明
  
- 命令的缩进，单词的大小写，空格的使用

- 注意看git给出的提示，很多的操作命令以及说明都会在提示里

- 文件内容最好是在本地修改，本地保存文件只要没有`git add file`就不会要求`commit`，而且还不用担心文件内容丢失

- 在github网页上每一次修改提交都会`commit`,`commit`多了看的有点晕，尤其是在没有注明修改注释时；怎么删除`commit`是个问题，有个优点就是修改后可以即时查看修改了哪些内容，修改的内容左边会有一条宽的竖线，红竖线代表修改前的内容，绿竖线代表修改后的内容，类似图形化的界面，看着更舒服，不像本地git命令行需要`git diff`

- 文件用英文方式命名，使用中文命名，在命令行`git status`时文件名显示为一长串的编码，后续操作很不方便

## Git常用命令

- [下载安装git](https://git-scm.com/downloads)

- 操作系统： Windows 7 64bit

- git version： 2.8.1

- 编辑器： Notepad++ v7.4.2

- 打开Git Bash,在命令行输入`cd`确认当前默认路径（已显示路径的可忽略这步）,使用`pwd`查看当前所在目录

		$ pwd
		/c/Users/Administrator

- 选择一个目录创建一个空目录，**使用英文命名**

		$ mkdir mystuff	# 创建一个叫mystuff的目录
		$ cd mystuff	# 打开mystuff目录,也可以打开已有的目录
		$ pwd			# 查看当前所在目录
		/c/Users/Administrator/mystuff
		$ git init		# 把当前目录变成Git可以管理的仓库
		Initialized empty Git repository in C:/Users/Administrator/mystuff/.git/

- 本地仓库已经有了，接下来就可以把文件放到这个仓库存起来，比如ex1.py:

		print "Hello World!"

- 将ex1.py存放在 C:/Users/Administrator/mystuff这个目录下(也是git的工作区)

	- `ls`查看目录下的文件名

			$ ls
			ex1.py
	- `cat`查看文件内容

			$ cat ex1.py
			print "Hello World!"

	- `git status`查看仓库目前状态，根据给出的提示，可以指导下一步的操作

			$ git status
			On branch master

			Initial commit

			Untracked files:
			  (use "git add <file>..." to include in what will be committed)

		       		 ex1.py

			nothing added to commit but untracked files present (use "git add" to track)

		注意看git给出的提示，有一个ex1.py的文件正等着提交到仓库，可以使用`git add <file>...`命令提交到仓库


			$ git add ex1.py	# 添加文件到仓库,可一次提交多个文件(ex1.py ex2.py ...)
			$ git commit -m "wrote a sentence"	# 提交文件到仓库并提交说明，方便以后查看

		这里提交到本地仓库有两个步骤，第一步是把文件给仓库管理员（暂存区），第二步是仓库管理员给文件做个记录并放入仓库（master分支）
		
- 继续编辑ex1.py

		print "Hello World!"
		print "Hello Again"

	- `git status`提示文件内容有修改，需要重新提交
	
	- `git diff HEAD -- ex1.py` 查看修改的内容

			$ git diff HEAD -- ex1.py
			diff --git a/ex1.py b/ex1.py
			index f4da9af..46d2b85 100644
			--- a/ex1.py
			+++ b/ex1.py
			@@ -1 +1,2 @@
 			print "Hello World!"
			+print "Hello Again"
			\ No newline at end of file

	- 使用`add`,`commit`提交修改后的文件即可
	
			$ git add ex1.py
			$ git commit -m "print again"

- ex1.py已经提交了两次，至此就已得到了关于ex1.py的两个历史版本

		$ git log	# 查看详细的提交记录
		$ git log --pretty=oneline	# 查看简洁的提交记录
		$ git reset --hard HEAD^	 # 回退到目前版本的前一个版本
		$ git reset --hard commit_id # 在版本的历史之间穿梭
		$ git reflog	# 查看命令历史
		$ git checkout -- file	# 丢弃工作区的修改，让文件回到最近一次commit或add是的状态
		$ git reset HEAD file # 丢弃暂存区的修改
		$ git rm file # 删除文件

### 通过ssh加密实现本地Git仓库和GitHub仓库之间的传输

- 在用户主目录下（/c/Users/Administrator），看看有木有.ssh目录，再看看目录下有木有`id_rsa`（私钥，自个使用）和`id_rsa.pub`（公钥，谁都可以知道）这两个文件。如果没有打开Git Bash，创建SSH Key：

		$ ssh-keygen -t rsa -C "youremail@example.com"

	一路回车，使用默认值即可。

- 登录GitHub，点击头像，打开"Setthings"->"SSH and GPG keys"->点"New SSH key"

	- "Title"添入备注
	- "Key"把公钥的内容写入(Ctrl C + Ctrl V)
	- 点"Add SSH kye"添加完成

	把需要同步的电脑生成的Key添加到GitHub，就可以在每天电脑上往GitHub推送了

- 