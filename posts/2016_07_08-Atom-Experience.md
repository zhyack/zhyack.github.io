# Atom 试用体验

偶尔浮出水面冒个泡...

[官网](https://atom.io/)

嗯，Sublime 既视感...   
好吧，其实我穷得根本用不起Sublime，跟风一波。  
  
作为开源的**编辑器**，感觉界面已经是很好了，比起win原装的记事本、笔记本，常见的编辑器notepad++、vim，IDE内置编辑器——Eclipse、VS内置，甚至是不是编辑器的编辑器emacs，都好看了一大截的说。  
但毕竟有一利必有一弊，比起记事本，notepad++这种运行起来要更废资源，毕竟要加载不少插件；比起vim，emacs这种又少了很多功能，并不能离开鼠标；而比起Eclipse，VS这些又没有代码提示，运行功能（其实是废话，人家只是个编辑器）。。。  
  
支持高亮的语言很多，而且插件还挺多，自动补全基本上也够用；支持多窗口(面板)，可以随意切分；支持Git状态实时显示；傻瓜安装好时基本功能就都有了，门槛够低。  
说说明显的缺点，预装的插件有很反人类的，比如whitespace，竟然自动把行尾空格去掉了，让我md文件情何以堪；同样是md预览，效果和markdownpad差了好多，基本不能用；很多其他插件应该也都有类似问题，功能不够完善，还处于发展中，不够成型；使用内置工具安装插件慢到死，安装需要VS编译器支持（要不是不知道什么时候装了个VS2013，我连插件都装不好？），然后高能一波手动安装插件时遇到的最大问题：<pre><code>apm install的时候出现以下错误：
gyp WARN install got an error, rolling back install
</code></pre>翻墙都没能解决，最后发现是编译器指定的有问题，默认的VS编译器是vs2012，我电脑上是2013，命令行中使用如下命令修改：<pre><code>apm config set msvs_version 2013</code></pre>
然后重新`apm install`，所有插件都很顺利地安装了。。。  
  
简单总结一下：  

* 好看。
* 作为编辑器插件够用。
* 耗电一般，比IDE省电，比弱鸡记事本耗电。
* 大文件能力，略逊于notepad++，略而已。
* 门槛低。

比较适合我目前的需求——笔记本不插电源时尽可能延长coding时间而又不失coding体验，尽可能提升装X技巧而又在强迫症等顽疾的容忍范围内。