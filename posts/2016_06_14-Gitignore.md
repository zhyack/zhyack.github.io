#.gitignore的使用
博主最近又手贱把本地的Eclipse Workspace删个精光，遗失了一些重要代码，又要耗费宝贵的娱乐时间去补窟窿。悔恨之余，决定用git把所有的代码都管理起来，不至于失去了才后悔莫及。  
于是问题来了——创建工程以及运行代码时生成的各种工程文件，编译文件，可执行文件，以及中途使用的一些数据文件，对我们而言并没有什么保存价值，琐碎的文件放在git里也会大大拖慢git的速度。我们想要的是保留指定后缀名的文件(如`.cpp`/`.java`)，使用`.gitignore`文件进行配置即可解决。  

* ##.gitignore文件  
	* 一般放在仓库根目录下进行全局设置，名为`.gitignore`，使用文本编辑器编辑即可。
	* 每行为一条设置，分为三种：
		* 以`#`开头——注释：如`#This is a comment`，一条注释而已。
		* 以`!`开头——保留：如`!.gitignore`，表示保留对.gitignore文件的管理。
		* 其他——忽略：如`.gitignore`，表示忽略.gitignore文件。
	* 非注释部分使用的是**glob**模式匹配。
* ##glob模式匹配
	* 与正则表达式相似，但及其简化，以至于部分功能难以实现。
		* `*`，表示0个或多个任意字符。
		* `?`，表示1个任意字符。
		* `[]`，与正则表达式的中括号类似，表示括号中的字符选其一。
		* 其他字符， 表示对应字符。
	* glob通配符在很多地方都有使用，如果之前没有了解可以回想一下。
*   ##Example
	*   将Eclipse的workspace做成git仓库，添加规则，即可实现仅保留对应源代码文件(`.cpp`/`.java`/`.py`等等)以及想保留的其他文件(放在每个二级目录的`data/`中)。
	<pre><code>#block all
	*.*
	#C/C++
	!*.cpp
	!*.c
	!*.cc
	#Java
	!*.java
	#Python
	!*.py
	#MarkDown
	!*.md
	#Web
	!*.html
	!*.htm
	!*.css
	!*.js
	!*.php
	#Data
	!*/data/*
	#Git
	!.gitignore
	</code></pre>

*   ##测试和提交
	* 在git控制台中 `git add .` 之后，使用`git status` 查看具体都add了哪些文件，如不满意，可使用 `git reset HEAD` 对 `add` 进行回退。
	* 测试合适之后就可以`git commit -m '...'`了。撤销`commit`可以用`git log`查看日志，然后选择之前的版本号`commit_id`用`git reset commit_id `进行回滚。

*  ##本地备份和远程备份
	* 上述做法只是本地使用git进行了版本控制，如果本地不小心删掉某个工程，便可使用版本号进行恢复。
	* 但如果手贱删的是整个仓库 :joy_cat: ...所以最好还是在网络上也做一个备份，比如Github的私有仓库，或者免费的Bitbucket私有仓库。只需要每次`commit`之后`push`一下就好了。
