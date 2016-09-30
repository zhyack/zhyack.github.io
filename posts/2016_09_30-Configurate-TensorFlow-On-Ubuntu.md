# 在Ubuntu环境下配置TensorFlow

* 系统: Ubuntu 16.04(64bit)
* Python: 2.7.12(Anaconda2)
* TensorFlow: 0.10.0(CPU)

* 准备工作
	* 下载安装Anaconda，[官网](https://www.continuum.io/downloads)，下载到本地使用命令`bash xxx.sh`安装。
	* 下载TensorFlow，[Ubuntu/Linux 64-bit, CPU only, Python 2.7](https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp27-none-linux_x86_64.whl)，[Ubuntu/Linux 64-bit, GPU enabled Python 2.7](https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.10.0-cp27-none-linux_x86_64.whl)，目前只实践了CPU版本的安装，GPU版本应该大致相同，只是要配置CUDA；故本文只谈CPU版本。
* 安装步骤
	* Anaconda的安装就略过吧，无脑装，只是注意最后一条提醒你加环境变量时记得输入`yes`，没有输入的就自行添加到.bashrc里吧。然后安装完要`source ~/.bashrc`，才能使Anaconda即时生效。
	* 输入conda试试，不是无效的命令即表示Anaconda装好了。
	* 第一条命令`conda create -n tensorflow python=2.7`，然后conda就开始给安装各种依赖的包了。这里可能出的问题全都是网络问题，网太差的就放弃吧...
	* 漫长(or短暂)的等待之后...
	* 第二条命令`source activate tensorflow` ，这句话其实是改变了环境变量，进入到所谓的tensorflow的环境变量配置中，其实也就是加上了tensorflow的路径而已。但是这样就可以通过`activate`和`deactivate`来控制是使用正常的python，还是tensorflow版的。所以退出tensorflow环境的命令就是`source deactivate tensorflow`。
	* **在tensorflow的环境中**，使用`pip install $DIR/tensorflow-0.10.0-cp27-none-linux_x86_64.whl`，其中`$DIR`就是你存放这个文件的路径啦。接着就是第二轮考验网速的时候。
	* 漫长(or短暂)的等待之后...
	* 装好了。。。
	* 进入python试一下吧，`import tensorflow`，没有错误提示就是成功了。
	* 此时在tensorflow环境中使用`conda list`可以看到刚才所有安装成功的包。退出tensorflow环境再试试？就没有刚才的包了。。所以只有在tensorflow环境内才可以用。

* 其他问题
	* 如果想卸载tensorflow怎么弄？
		* **在tensorflow环境中**， `pip uninstall tensorflow`，如果提示你本来就没有tensorflow，那可能是各种原因tensorflow不在环境变量里，关掉terminal重开，重新`activate`，然后卸载。
	* 如果想更新tensorflow怎么办？
		* 先卸载，再安装。按以上方法卸载旧版本，然后关掉terminal重开，使其重新加载环境变量，然后安装新版本。
	* tensorflow在哪儿？
		* ~/anaconda2/envs/tensorflow
		* 对应github上的库 ~/anaconda2/envs/tensorflow/lib/python2.7/site-packages/tensorflow
	* ...

总体来说跟安装Theano差不多，Anaconda真是个省事儿的好东西呀...
