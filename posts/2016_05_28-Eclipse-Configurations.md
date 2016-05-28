#Eclipse各种环境的搭建
虽然现在搭这些环境已经是驾熟就轻了，但各种插件的网址也是记不清，每次都要查一遍，所以写个小结记录下。对于初学者来说也会有所裨益吧。  

>  默认Windows系统，虽然Eclipse跨平台，但由于系统环境不同，在Linux系统上也会稍有一些区别，在介绍时会尽量顾及。  
>  虽然官网上提供供各种开发用的Eclipse版本（其实也就是装好各种插件的），但毕竟很多时候我们要使用多种语言，总不能桌面上摆三个快捷方式——Eclipse\_JAVA，Eclipse\_C++，Eclipse\_Python吧。
 
* ##JAVA
	*  Java当然是默认就有的，[官网](http://www.eclipse.org/downloads/)上即可下载，认字的自己选择了，不认字的直接点[这个](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-java-mars-2-win32-x86_64.zip)吧。  
	* 如果装好还运行不了Java程序，你需要装JDK和JRE...一般来说，下载[JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)安装即可，安装完之后如果还不能运行，那应该是系统环境变量没有自动配置，添加类似如下环境变量：
	<pre><code>新增JAVA_HOME=C:\Program Files\Java\jdk1.8.0_91
新增JRE_HOME=C:\Program Files\Java\jre1.8.0_91
CLASSPATH中添加C:\Program Files\Java\jdk1.8.0_91\lib 和 C:\Program Files\Java\jre1.8.0_91\lib
path中添加C:\Program Files\Java\jdk1.8.0_91\bin
	</code></pre>
	* 重开Eclipse，JAVA可以运行了。
* ##C/C++
	* ###安装CDT
		* [官网](http://www.eclipse.org/cdt/downloads.php)中有安装文件下载，找到对应版本的仓库url，比如Mars.2版本的( http://download.eclipse.org/tools/cdt/releases/8.8.1)。
		* 打开Eclipse，Help->Install New Software->Add->Name:cdt , Location: http://download.eclipse.org/tools/cdt/releases/8.8.1, 然后选cdt基础包，一路next即可。
		* 现在应当是可以建C++工程了，但并无卵用，不能运行，因为你的系统中还没有C++的编译环境——g++。

	* ###安装g++
		* [官网](https://sourceforge.net/projects/mingw/files/Installer/)，下载mingw-get-setup.exe，运行选择需要的东西，比如base包，g++包，gcc包等，傻瓜式安装即可。
		* 安装完之后记得检查系统变量path中是否存在`C:\MinGW\bin`类似物，没有就添上。
		* 重启Eclipse新建工程尝试下能否运行C++程序，不能的话就重启下电脑，更新下环境变量。
		* GDB已经装好了的说...	

	* ###linux版本
		* linux稍有不同，g++是可以直接`apt-get install`的，但需要在Eclipse->Window->Preferences->C/C++->New C\C++ Project Wizard 中设置ToolChains为默认MinGW GCC，然后重启生效。 
* ##Python
	* ###安装Pydev
		* [官网](https://sourceforge.net/projects/pydev/files/pydev/)有各种版本，不过还是推荐使用url(pydev - http://pydev.org/updates)类似cdt的安装方式进行安装。
		* 装完当然是不能运行python的...
	* ###安装python
		* [官网](https://www.python.org/downloads/)，无脑装...
		* 这个还真不用配环境变量，但是需要下面步骤。
	* ###配置python
		* Eclipse->Window->Preferences->Pydev->Interpreters->Python Interpreters->New，找到python.exe的位置，选中加入，Apply，搞定。
		* 可以跑python了。
* ##其他
	* 更为复杂的环境搭建，举个例子，[Theano](https://zhyack.github.io/posts/2016_05_26-Configurate-Theano-On-Windows.html)。
	* 但其实搭这些环境都是一回事儿了，插件安装+软件依赖+环境变量。
	