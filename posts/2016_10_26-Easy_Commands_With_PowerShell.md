# Atom中使用PowerShell

工欲善其事，必先利其器...

## 安装
* 借助插件`platformio-ide-terminal`，在之前的[Atom配置](https://zhyack.github.io/posts/2016_09_24-Atom-Config.html)中已经详细介绍了，此插件默认使用的是Windows自带的PowerShell。

## 使用
* 用`platformio-ide-terminal`基本两个命令就够用了
	* **Ctrl+`**——打开和隐藏terminal
	* **Atl+Shift+X**——关闭terminal
* 要使PowerShell用起来更方便，简单暴力的两大利器
	* **Set-Alias**
		* Alias和linux的alias功能基本一样，但问题在于其只能基于已有功能重新命名短名，而不能产生新的功能。
		* `Set-Alias $name $command`——设置alias
		* `del alias:$name` ——删除相应的alias
		* Alias的功能在Function中均可实现，故不多赘述
	* **Function**
		* 定义自己的函数 ，形式如此——`function $FUNC_NAME ($A1,$A2,...$AN[="default value of $AN"]){codes, one command per line}`
			* 整体和C/C++的函数形式比较像
			* $FUNC_NAME——方法名称，之后再powershell输入名称即可调用函数。
			* $A1...$AN——“内部参数”， 可以指定默认值， 使用的时候需要带`-`来指定参数，如`git commit -m "..."`中的`-m`即是指定内部参数`$m`的值为后面的字符串。在函数体内用`$A1`的形式调用参数。
			* args——“外部参数”，是调用函数是临时跟在函数名后的参数，如`sum 12 34`中的`12 34`就可以在`sum`的函数体中使用`$args[0]`和`$args[1]`调用。
			* 函数体部分，以换行分隔指令，具体怎么写可以随意发挥；相当于$FUNC_NAME这个函数包裹了整个代码段的各种命令，所有的命令均会各自执行且输出。
		* 如果代码段只有一行推荐整体写为一行。
		* function可以直接在terminal中输入执行，但仅限当前回话有效，关闭后即失效。
	* 使`Set-Alias`和`Function`永久生效
		* 方案一——直接去改PowerShell的全局配置，从权限、安全、方便的角度考虑，都是及其不推荐的，也不做介绍。
		* 方案二——修改用户配置
			* 默认的用户配置路径是`$home/Documents/WindowsPowerShell/`。其中`$home`是你的用户文件夹`.../users/XXX/`
			* 在`$home/Documents/WindowsPowerShell/`下建一个名为`Modules`的文件夹，然后在这个文件夹中放入你自己的`module`。
			* 所谓`module`是你自己定义的函数、变量、配置等的集合，就如同python中的`import`的包，你的`module`中包含了你需要的各种东西。当然目前也不需要用到很多，暂时认为一个`module`是一个内有各种function的文件夹即可。
			* 此时在`$home/Documents/WindowsPowerShell/Modules/mymodule/`下建文件，命名为`mymodule.psm1`(mymodule是你的module名字，自行替换)，在这个文件中写上你所有实现的函数。比如<pre><code>function gpush($b="master",$m="auto_push"){
				git checkout $b
				git add .
				git status
				git commit -m $m
				git push origin $b
}</code></pre>
			* 保存好后可以开一次PowerShell试试，这个时候应该是没有任何效果的。但如果使用命令`Import-Module mymodule`，就可以将mymodule加入到当前会话的配置，这个时候使用gpush就可以一口气push了~ 但是关闭后重新打开，就又不行了。
			* 所以我们需要设置PowerShell每次打开时自动加载我们的mymodule——在`$home/Documents/WindowsPowerShell/`下新建文件`profile.ps1`，写入<pre><code>Import-Module mymodule
Import-Module Microsoft.PowerShell.Management
Get-Module</code></pre>重新打开PowerShell，`Get-Module`让PowerShell一打开就显示出加载好的Modules，自定义命令玩起来~
			* 之后添加自定义命令只需更新`mymodule.psm1`然后重启PowerShell即可。
		*  如果提示没有权限运行脚本，可以使用命令`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`来改变当前用户的权限。
