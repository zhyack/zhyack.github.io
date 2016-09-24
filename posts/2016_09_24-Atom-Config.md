#Atom轻便型环境配置  
最近把Atom进行了初步配置，感觉不错，记录一下。
	
* ### Settings
	* `Ctrl+,`进入总体设置。
		* `Core`中勾上`Aoto Hide Menu Bar`，去掉`Remove Empty Pane`
		* `Editor`中`Font Size = 14`，勾选`Soft Wrap`和`Soft Wrap At Preffered Line Length`，`Tab Length = 4`
* ### Packages 
	这才是重点...  
	* autocomplete系列
		* autocomplete-java，autocomplete-python，autocomplete-json，language-matla，autocomplete-clang，linter-clang，clang-format，etc.
		* 不用调整设置，直接装上就好了。
	* 工具系列
		* expose——无须调整，`Alt-Shift-E` 实现窗口选择。
		* hyperclick——无须调整，按住`Ctrl`点击变量函数名就可以查到定义处，必装...
		* platformio-ide-terminal——按`Ctrl+`` 调出底部PowerShell，内置控制台，必备...
			*   设置中，去掉`Run Inserted Text`， `Default Panel Height = 150px`，`Font Size = 12px`， `Theme`选`dracula`
			*   `Custome Texts`自己填啦，填好后在config文件夹(`C:/User/XXX/.atom/`)中`/packages/platformio-ide-terminal/keymaps/platformio-ide-terminal.cson`中`'.platform-linux atom-workspace, .platform-win32 atom-workspace':`下加入几行设置<pre><code>'ctrl-shift-1': 'platformio-ide-terminal:insert-custom-text-1'
  'ctrl-shift-2': 'platformio-ide-terminal:insert-custom-text-2'
  'ctrl-shift-3': 'platformio-ide-terminal:insert-custom-text-3'
  'ctrl-shift-4': 'platformio-ide-terminal:insert-custom-text-4'
  'ctrl-shift-5': 'platformio-ide-terminal:insert-custom-text-5'
  'ctrl-shift-6': 'platformio-ide-terminal:insert-custom-text-6'
  'ctrl-shift-7': 'platformio-ide-terminal:insert-custom-text-7'
  'ctrl-shift-8': 'platformio-ide-terminal:insert-custom-text-8'</code></pre>然后在`/packages/platformio-ide-terminal/menus/platformio-ide-terminal.cson`中靠近结尾的地方添加以下设置，具体位置应该一看就明白了<pre><code>{
          'label': 'Insert pre-1'
          'command': 'platformio-ide-terminal:insert-custom-text-1'
        }
        {
          'label': 'Insert pre-2'
          'command': 'platformio-ide-terminal:insert-custom-text-2'
        }
        {
          'label': 'Insert pre-3'
          'command': 'platformio-ide-terminal:insert-custom-text-3'
        }
        {
          'label': 'Insert pre-4'
          'command': 'platformio-ide-terminal:insert-custom-text-4'
        }
        {
          'label': 'Insert pre-5'
          'command': 'platformio-ide-terminal:insert-custom-text-5'
        }
        {
          'label': 'Insert pre-6'
          'command': 'platformio-ide-terminal:insert-custom-text-6'
        }
        {
          'label': 'Insert pre-7'
          'command': 'platformio-ide-terminal:insert-custom-text-7'
        }
        {
          'label': 'Insert pre-8'
          'command': 'platformio-ide-terminal:insert-custom-text-8'
        }</code></pre>
			* 每次重新设置插入文字之后都要重启才能继续使用快捷插入；这个功能还是相当有用处的，编译，运行什么的都可以快速搞定了。
	* 预览系列
		* markdown-preview-plus——在md文件中按`Ctrl+Shift+M`可以调出预览窗口，画风比较朴实，功能并不完全，常用md记简单笔记的推荐安装。
		* atom-webbrowser——内置浏览器，其实对于企图用编辑器搞定一切问题的人们来说这是迫切需要的，然而本人表示已卸载，真的是不好用，不好用，不好用。。。
			* 执意要用的，记得在config文件夹中`styles.less`中添加以下设置<pre><code>atom-webview { height:100%; }</code></pre>这样才能全屏啊。。。
			* 不管地址栏里填什么都是打开默认的`github.com`，无语了，每次还都要开新窗口，完全不受控制，希望以后的版本能好好改下BUG吧。。。
	* 装X系列
		* activate-power-mode——点到Install里第一个就是它了，为什么这么火自己试下就清楚了。。。
	* 其他(未完待续)

经过简单配置，基本可以轻松使用Atom替换IDE了，容易上手，很节能，而且`F11`+`Alt`之后全屏界面挺不错的。  
不过Atom的各种奇葩的问题也是常有的，毕竟是组合体，遇到异常情况一定要先试试重装package以及重启Atom。。。

* ###Bug收集与应对
	* 用了一段时间后发现，Atom自动升级后，并非直接替换原版本，而是直接下了一个新版本的文件夹放在那里，注册表中version改成新版本，但**路径没改！！！**真是醉了。  
	具体表现为文件夹右键`open with atom` 失败，快捷方式失败，自定义的打开方式失败(如我的rainmeter)；而且它还会暂时保存上个版本的文件，结果就是某些快捷方式虽然能打开，但是各种问题。。。所以升级后打不开也算是正常了。应对方案如下：
		* 首选明确其主体文件路径，一般是`C:\Users\XXX\AppData\Local\atom`，AppData是隐藏文件夹，你懂的。。 其中会有不同的版本以`app-1.xx.x`文件夹命名，里面有对应的exe文件。
		* `Win+R`+`regedit`打开注册表， 直接`Ctrl+F`搜索'atom'，注意搜索框只勾选`项`和`全字匹配`，然后搜到哪儿改到哪儿，就是改路径，看到路径就改成新版本的，就算搜到的项没有路径展开后子项也一定会有路径的，改改改。。。
		* 现在应该可以正常使用了，- - .