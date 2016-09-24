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