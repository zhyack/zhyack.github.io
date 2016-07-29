#简单便宜的VPS搭建体验
* 平台： DigitalOcean
* 系统： Ubuntu16.04
* 配置： 512MB RAM，20GB SSD，1TB流量，支持ipv6
* 收费： $5/月，实际按$0.007/小时，随时更换服务器，合理方便
* 用途： VPN，个人网站等...
* 本文适合人群： 懂点英文想科学上网或建站而又嫌麻烦/贵的高校学生

##优惠
* [Github Educational Pack](https://education.github.com/)，学生特惠，凭高校邮箱申请，如果被拒可以直接发邮件或者在[这里](https://education.github.com/contact)合理申诉，说理中肯且表达出急切的心情即可。前几年还是$100的优惠，现在只有$50了，不过也很不错了，够几乎免费用1年了（长时间不用的时候可以备份后删机器，之后不扣费）。  
* 就算不是学生也是可以蹭些优惠的，比如通过[邀请链接](https://m.do.co/c/7016e14563dd)注册，可以获得$10的优惠，两个月免费，就算初始激活交$5，那也是三个月用￥30左右，还是比市面上的VPS和VPN便宜的多的。而且，这个其实多注册几个账号也可以的吧，只要注册时机器，邮箱，使用的paypal等不同即可避嫌，对于可以获得一个好用的server来说，麻烦一点点还是很值得的。

##激活
* [官网](https://m.do.co/c/7016e14563dd)先摆上，注册登录会提示使用信用卡或paypal激活。
* 信用卡：这个基本不适合天朝人民，穷人表示根本没见过VISA、Mastercard云云。鉴于激活比较困难大都是学生，推荐用paypal激活。另外绑定信用卡貌似解绑比较费劲，不如paypal来的灵活。
* paypal：**你需要一张62开头的开通了网银的银联信用卡/借记卡**，一般高校学生都是学校发的借记卡。随便去[官网](https://www.paypal.com/)注册个号，然后添加你的卡。 在DigitalOcean上选择paypal支付$5激活，然后顺着交费就可以了。（博主在这里遇到些麻烦，主要是paypal有点抽风，有时候可以顺利到网上银行交费界面，有时候就弹出错误，如果出错就过几个小时重新试一下，但要注意——62开头、开通网银、信用卡/借记卡）
* 激活之后在[Billing界面](https://cloud.digitalocean.com/settings/billing)添加Promo Code，也就是之前Github Educational Pack中包含的优惠码，即可直接在账户上多出优惠的钱了。（注意优惠的钱是有时限的，大概两年？博主之前一个$100的优惠过期了，心好痛。。。）

##服务器
* DigitalOcean上叫Droplets，在[creat界面](https://cloud.digitalocean.com/droplets/new?size=2gb)可以看到各种系统、各种配置的、甚至各种预配置的环境的，根据所需选择，一般$5/mo的方案是够用的。
* 至于节点，不建议听网上那些San Francisco党，博主测试下网通最快的大概是New York 2/3这两个节点。推荐根据自己的网络在[这里](http://speedtest-sfo1.digitalocean.com/)测速，选择比较快且稳定的节点。
* ipv6根据选择勾选，其他都不用勾选。
* 确认后DO会帮你创建一台服务器初始环境，账号root，ip和密码都会发送到你的邮箱。使用putty类似的东西都可以登陆，首次登陆会让你先改密码，改完就看下面。
##科学上网
* 此处是Ubuntu系统搭建shadowsocks的笔记，其他需求自行谷歌。
* 过程很简单！！！只需利用pip直接安装shadowsocks，所以就是安装pip，安装shadowsocks，启动，完事儿。<pre><code>apt-get install python-pip
		y
pip install shadowsocks</code></pre>

* 然后就可以用`ssserver -p _PNO -k _KEY -m rc4-md5 -d start`，启动了，其中`_PNO`指的是端口号，比如`8000`；`_KEY`指的是密码，自行设置。关闭服务就是把`start`改成`stop`。
* 为了方便还可以这样:<pre><code>sudo vim /etc/bashrc
添加：
		alias sss="ssserver -p 8000 -k XXXXXX -m rc4-md5 -d start"
		alias sse="ssserver -p 8000 -k XXXXXX -m rc4-md5 -d stop"
source /etc/bashrc</code></pre>然后就可以在terminal用sss，sse来开关了。
* 在本地使用shadowsocks客户端，[官网链接](https://shadowsocks.org/en/index.html)。打开后对应填入你的服务器ip，端口号，密码等信息，然后启用系统代理，可以科学上网了。
* 本人体验——速度不算飞快，但可以满足需求。直观一点的话——youtube上720P无压力，1080P偶尔卡。IPv6网站可以访问，但是速度较慢，而且pt下载没有速度，暂未解决，考虑用服务器中转。目前毫无优化，如尝试优化后效果不错就回来补上笔记。

##建站
* `apt-get install apache2`，`cd /var/www/html/`
* 好了，别打脸，其实就是你能想到的都可以在服务器上试，注意配置限制。