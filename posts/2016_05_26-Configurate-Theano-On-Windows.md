#Windows下Theano环境搭建
* 系统： Windows 8/10 (64位)
* Python： Anaconda2-4.0.0-Windows-x86\_64 (python 2.7.10)
* CUDA： Cuda_7.5.18
* VS：VS2013

Theano也算是深度学习主流工具之一了吧，其优势主要在于使用简单——普通的python语法，CPU/GPU无脑切换。在不过分苛求运行速度的情况下，Theano是不错的选择。不过其环境搭建也如同各种工具一样，到处都是坑。  

* ##准备工作
	* 如果想尽可能简单地进行，**建议**在一切开始前卸载系统中所有python和MinGW g++，特别注意从环境变量中除去它们，然后重启。不过，不是必要的。
	* 下载[Anaconda](https://www.continuum.io/downloads)，[CUDA](https://developer.nvidia.com/cuda-downloads)，[VS](https://www.visualstudio.com/)。
	* 准备测试用的代码，比如[这里](http://deeplearning.net/tutorial/)随便一个模型的代码。
* ##安装Anaconda
	*  傻瓜式安装之后，打开cmd，输入`conda install mingw libpython`，等待...然后输入`pip install theano`，再等待...
	*  把Anaconda相关的路径添加到环境变量`path`中<pre><code>C:\Anaconda\MinGW\x86\_64-w64-mingw32\include;
	C:\Anaconda\MinGW\x86\_64-w64-mingw32\lib;
	C:\Anaconda\MinGW\bin;
	C:\Anaconda;
	C:\Anaconda\Scripts;</code></pre>
	* 然后重开个cmd，输入`python`，应该会出来Anaconda Python的命令行界面，然后输入`import theano;`，应该不会提示有什么错误。如果提示各种错误，看看错误日志很快就能发现问题的，一般都会提示哪里遇到了什么东西找不到的错误，对应检查一下环境变量。如果有其他版本的MinGW或python，也有可能导致错误。
	* 这时尝试运行代码，比如cmd中`python lstm.py`，大概是会报错的 :smirk\_cat: 。
	* 在用户目录下（比如`C:\Users\zhy\`）新建一个文本文件，命名为`.theanorc.txt`，然后如下编辑保存，再次在cmd中运行，应当是可以用cpu跑起来theano了<pre><code>[global] 
	openmp = False 
	device = cpu 
	floatX = float32 
	allow\_input\_downcast=True 
	[blas] 
	ldflags= 
	[gcc] 
	cxxflags=-IC:\Anaconda\MinGW\x86\_64-w64-mingw32\include</code></pre>
* ##安装CUDA
	* 傻瓜式安装的说...
	* 环境变量应当是自动配置好的，以防万一，还是检查一下：<pre><code>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v7.5\bin;
	C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v7.5\libnvvp;</code></pre>
* ##安装VS2013
	* 无脑装...
	* 如果只是为了搭theano环境的话把c++相关的内容装上即可，其他臃肿的东西可不选。装VS完全就是为了编译器。
* ##GPU运行Theano
	* 很简单，改下配置文件`.theanorc.txt`即可:<pre><code>[global] 
	openmp = False 
	device = gpu 
	floatX = float32 
	allow\_input\_downcast=True 
	[blas] 
	ldflags= 
	[gcc] 
	cxxflags=-IC:\Anaconda\MinGW\x86\_64-w64-mingw32\include
	[nvcc] 
	flags = -LC:\Anaconda\libs --cl-version=2013
	compiler\_bindir = C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\amd64 
	fastmath = True </code></pre>
	* 改变的主要是[nvcc]的选项，如果用的是VS2012的话就对应修改`-version`和`compiler_bindir`的对应部分就行。网上也有各种版本的配置文件，经常出问题的地方也都是VS编译器的路径没指对（不知道他们是怎么搭好环境的 :speak\_no\_evil: ）。

* ##安装cuDnn
	* 这个东西跑LSTM并没有看出优势。。但CNN应该应当是会效果很好。
	* [官网](https://developer.nvidia.com/cudnn)下载cnDnn的库，其实也就是一个压缩包，三个文件。对应文件解压到之前CUDA安装的文件夹相应位置中就可以了。
	* 然后改下配置文件`.theanorc.txt`（尾部添加），就可以自由控制是否使用cuDnn了，使用的时候就是True，不用就是False。:
		<pre><code>[dnn]
enabled = True
</code></pre>
	
* ##摆脱控制台操作  
博主个人喜欢Eclipse的编辑器，没错——是编辑器。而Eclipse又是个什么都能跑的IDE，所以个人推荐Eclipse。如果上面步骤进行的都很顺利，那用Eclipse跑Theano也很容易配置。
	* Eclipse装PyDev，略。
	* 配置PyDev的Python Interpreter，指向Anaconda根目录的python。
	* 建个工程，放进去测试代码，运行一下... :smirk\_cat: 
	* 经实验，Eclipse的环境变量应当是系统启动时随系统环境变量更新，而刚才配置的环境变量还没有应用的Eclipse中，所以——重启一下，再试一次。 :neutral_face: 


 