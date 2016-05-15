# 在静态博客中添加Emoji表情组  
　　随着站点一点点地搭建起来，博主所期望的站点功能也是越来越完善。如今网络语言中各路表情被广泛使用，能达到“一图胜千言”的效果。博文中虽然不要求那么丰富的表情元素，但基础的小表情组应当是必需的，比如，Emoji表情组—— :joy: 。  

* Emoji表情包  
　　Github上很多emoji相关项目中都存有完整的表情包，推荐[EMOJI CHEAT SHEET](https://github.com/arvida/emoji-cheat-sheet.com/tree/master/public/graphics/emojis)——881个表情，5.55MB，相当清晰，以表情内容命名，方便查找引用。更重要的是其[主页](http://www.emoji-cheat-sheet.com/)提供了emoji速查表，初期能让使用相当便利。  
　　把整个包下载之后，挑出表情包的文件夹(emojis/)放入自己静态博客项目中，例如本博客放在了`../pics/emojis/`（从[我的github项目](https://github.com/zhyack/zhyack.github.io)中抽取emojis包也是可以的）。  
* 表情的使用  
　　当然有了表情图片我们是可以直接按普通图片用的，但会存在一些问题——图片大小需要调整；对齐需要调整；路径太长，大量引用时很不方便。于是需要一种能方便快捷输入编辑这些图片的方法。  
　　思考对这些图片的使用时代码的共同点——标签，样式，路径...除了名字外其他全都相同，可以统一设置。所以我们需要一种能够将其名字作为关键字替换成相应代码的工具，自己实现起来还是要费一番功夫的，还好已有前辈提供了开源的工具——[emojify.js](https://github.com/Ranks/emojify.js)。
* emojify.js  
　　1.在其项目中提取emojify.js或emojify.min.js，放入自己项目中。  
　　2.在自己网站的css文件，例如style.css中添加emoji的样式。  
　　3.在使用emoji的网页</body>之前添加对emojify.js的脚本引用，而且还要添加一段激活emojify的脚本代码。  
　　4.使用时务必注意冒号前后的空格，比如`:joy:`是不会显示图片的，html中写成`(空格):joy:(空格)`即可显示为 :joy: ，本地用浏览器测试或提交到网站查看效果。
<pre><code>style.css中追加：
	.emoji {
	width: 1.5em;
	height: 1.5em;
	display: inline-block;
	margin-bottom: -0.25em;
	}
html中</body>前添加：
    < script src="../javascripts/emojify.min.js"></script>
    < script src="../javascripts/emojify.run.js"></script>
**ps注意粘贴时去点script前的空格。
其中emojify.run.js是自己创建的js文件，代码为：
emojify.setConfig({
	emojify_tag_type : 'section',           // Only run emojify.js on this element
	only_crawl_id    : null,            // Use to restrict where emojify.js applies
	img_dir          : '../pics/emojis',  // Directory for emoji images
	ignored_tags     : {                // Ignore the following tags
		'SCRIPT'  : 1,
		'TEXTAREA': 1,
		'A'       : 1,
		'PRE'     : 1,
		'CODE'    : 1
	}
});
emojify.run();
按自己情况修改上述代码中的emojify_tag_type和img_dir。
如果不想另外创建js文件，也可以直接在html中对应位置放上上述代码。
</code></pre>
　　