#Ubuntu服务器命令行安装Matlab
说起来在Linux上装各种神奇的工具包，真是让大家都挺抓狂的一件事。系统环境，依赖关系，冲突，命令行，sudo权限等等，哪一环节有问题都是很大的麻烦。apt-get固然方便，然而很多工具并没有包括，就算有也一定不是最新的，所以很多东西还是要下载到本地自行配置的，比如——Matlab。  
首先声明参考[链接](http://www.aichengxu.com/view/39100)在此。  

* Ubuntu 系统 14.04 server
* Matlab 版本 2014b + crack文件
* Java 版本 JAVA 1.7(7u71)

然后一步一步操作：

###安装JAVA

这个还是很简单的，JAVA是免费的，从官网上找到对应版本的tar.gz包下载即可，这里因为不知道java1.8对Matlab2014b的支持如何，所以还是安装了1.7版本的java。

* 下载java包(JRE和JDK)到本地，解压到/usr/lib/jvm/
* 设置环境变量，在~/下的.bashrc中添加  
<pre>
    export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_71  
    export JRE_HOME=/usr/lib/jvm/jre1.7.0_71  
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
    export PATH=${JAVA_HOME}/bin:$PATH 
</pre>
* 终端中`source ~/.bashrc`，使其生效即可，之后可以使用`java -verion` 查询java版本。

###镜像及破解文件下载

暂时先用出处的[链接](http://bbs.feng.com/read-htm-tid-8467093.html)吧。下载R2014b\_glnxa64.iso，MATLAB\_R2014B\_MAC\_LINUX\_crack.zip，以及libmwservices.so.rar。  
其中镜像文件解压(尽量不要挂载)在本地，以下此路径简写为\_MATLAB，crack文件解压路径简写为\_CRACK，libmwservices.so解压路径简写为\_LIBSO。

###安装
* 创建安装目录  
<pre>
    sudo mkdir -p /usr/local/matlab/etc  
    sudo mkdir -p /usr/local/matlab/2014b
</pre>
* 编辑配置文件   
<pre>
    sudo cp _MATLAB/installer_input.txt /usr/local/matlab/etc  
    sudo cp _MATLAB/activate.ini /usr/local/matlab/etc  
    sudo cp -r _CRACK/ /usr/local/matlab/etc 
</pre> 
* 修改文件的读写属性 
<pre>
    sudo chmod +w /usr/local/matlab/etc/installer_input.txt  
    sudo chmod +w /usr/local/matlab/etc/activate.ini  
</pre>
* 编辑installer\_input.txt文件，按如下内容设置配置项   
<pre>
    destinationFolder=/usr/local/matlab/2014b #安装目录  
    fileInstallationKey=  29797-39064-48306-32452 #序列号  
    agreeToLicense=yes #同意协议  
    outputFile=/tmp/mathwork_install.log #安装日志  
    mode=silent #开启无人值守安装  
    activationPropertiesFile=/usr/local/matlab/etc/activate.ini #激活文件  
    licensePath= /usr/local/matlab/etc/license.lic #license文件  
</pre>
* 替换java/jar/install.jar  
把_MATLAB下的 java/jar/install.jar 替换为 _CRACK中的 install.jar。

* 安装  
<pre>
    sudo _MATLAB/install -inputFile /usr/local/matlab/etc/installer_input.txt
</pre>
###破解
* 编辑activate.ini文件，按如下内容设置 
<pre>
    isSilent=true #开启silent模式  
    activateCommand=activateOffline #设置激活方式, 离线激活 无需联网  
    licenseFile=/usr/local/matlab/etc/license.lic #license文件位置  
</pre>
* 替换libmwservices.so  
<pre>
    sudo mv /usr/local/matlab/2014b/bin/glnxa64/libmwservices.so /usr/local/matlab/2014b/bin/glnxa64/libmwservices.so.bak  
    sudo cp _LIBSO /usr/local/matlab/2014b/bin/glnxa64/
</pre>
* 破解  
<pre>
    sudo /usr/local/matlab/2014b/bin/activate_matlab.sh -propertiesFile /usr/local/matlab/etc/activate.ini 
</pre>
###设置环境变量
 在~/下的.bashrc中添加：
<pre>
    export MATLAB_HOME=/usr/local/matlab/2014b  
    export PATH=${MATLAB_HOME}/bin:$PATH
</pre>
然后 
<pre>
    source ~/.bashrc
</pre>
大功告成~

在终端输入`matlab` 测试能不能进入matlab的控制台吧。

ps：如果没有sudo权限，JAVA和MATLAB都安装在用户目录下即可，不需要权限，然后环境变量配置成临时变量。以上步骤配置的JAVA和MATLAB都是用户级的，全局设置需修改/etc下的环境变量文件。