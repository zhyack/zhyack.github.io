#利用计划任务提交本地仓库到Github
妈妈再也不用担心我丢进度了~  

* 你是否期望一键push到Github？
* 你是否期望定时push到Github？

往下看吧...

* ##利用bat一键push
	* 现学现卖——`start 程序名` 类似地就相当于开了个cmd窗口，然后执行`程序名`。所以，我们只要把git的路径(比如`D:\Program Files\Git\bin`)添加到系统环境变量`path`中使得cmd可以找到`git.exe`就行了。然后在某个地方创建一个bat文件，添加如下内容：<pre><code>start /wait git add .
start /wait git commit -m "autoUpd"
start /wait git push origin master</code></pre>
	其中`/wait`是要等这个程序执行完才执行下一句。  
	* 如上就有一个问题了——如果当初你`git clone`这个要提交的仓库时用的是https://，那就会提示你输入用户名和密码，这\*\*就尴尬了。为了方便，我们要将此仓库设置为经ssh提交：
		* 不想重新clone的话就改下仓库根目录下`.git/config`文件如下位置<pre><code>[remote "origin"]
	url = git@github.com:USERNAME/REPONAME.git  </code></pre>
		替换一下你自己的USERNAME和REPONAME吧。
		* 然后根据[官网](https://help.github.com/articles/generating-an-ssh-key/)的步骤生成ssh key以及设置。  
		**注意：**不要受其蛊惑而设置`passphrase`，我们一切为了方便，`passphrase`设为**空**，否则你又该受到每次都要 输入`passphrase`的困扰。
	* 在cmd中或直接运行.bat文件试试，应该可以自动push了吧。
* ##利用计划任务定时push
	* Windows计划任务，傻瓜式操作，按自己需求添加即可，不会就去问度娘吧。
	* 需要一提的是：Windows计划任务打开的cmd默认目录是C:/System32/，这儿又没有仓库...于是需要简单修改一下bat文件，使其cmd可以进入指定仓库的目录，比如：<pre><code>cd C:\Users\xxx\yyy\REPONAME\
start /wait git add .
start /wait git commit -m "autoUpd"
start /wait git push origin master
pause</code></pre>
	pause一下你就可以观察提交记录了。嗯，就是这样。
	