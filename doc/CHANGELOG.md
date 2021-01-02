##  增加了valine魔改版具有以下特性：
 1. 支持个性标签，如博主，小伙伴，访客等，可自定义
 2. 支持自动识别qq账号
 3. valine使用前需要在leancloud注册账号，获取appid和appkey，添加到butterfly下的_config.yml的对应配置下
```
valinex:
  appid: [appid]
  appeky: [appkey]
  master: 博主qq的md5字符转
  friends: 
    - friend-md5
    - friend2-md5
    ....
```

##  可添加valine评论自动提醒（qq，微信） | 此魔改有些难度，如果不能独立解决问题，建议不要盲目改动
 * 需要将自动提醒后台部署到leancloud（国际版）
为什么是国际版，因为可能会牵扯到自定义域名，而国内版自定义域名是强制备案的，呵呵。。。

从此链接[LeanCloud](https://leanapp.cn/)进入到leancloud官网，在导航栏有国际版字样，点击cosole，跳转到国际版leancloud的登陆或注册页面，这时候应该会让你注册，然后登陆，创建应用需要先填写手机号，邮箱，并验证，通过后就可以使用，国际版也是中文的，无需担心。
然后，在左侧菜单设置-》应用keys，可以看到appid和appkeys，创建个txt保存下来，用于valine的配置。

下一步，左侧菜单云引擎-》部署-》点击部署项目，选择git部署，不选中自动部署，远程仓库填写***https://github.com/sviptzk/Valine-Admin-Server.git***，选择生产环境，分支是master，然后点击部署，等待一会，就会出现部署完成字样，然后我们到云引擎-》设置的最下面填写云引擎域名,
随便起，只要不重复就可以，然后就可以用 '你使用的云引擎域名'+'.avosapps.us'+'/sign-up'就可以登录到评论管理登录页面，第一次进入会让你输出邮箱和设置密码，以后就可以用'你使用的云引擎域名'+'.avosapps.us' 或者 自定义域名 直接登录。

第二步，云引擎-》创建定时任务

由于免费版会不定时强制睡眠，所以需要定时唤醒
定时检查24小时内漏发的邮件通知
生产环境选择resend_mails
选择Cron表达式时间自己调整0 0 1 * * *

自动唤醒
生产环境选择self_wake
选择Cron表达式时间自己调整0 0/60 0 * * ?

第三步设置白名单，在左侧菜单的设置-》安全中心-》安全域名下填写需要通过的url

第四步，填写自定义环境变量
在云引擎-》设置创建多条自定义环境变量，按照如下填写

> tip： 每一次修改环境变量需要重新部署一次（重启小按钮）

|变量名|	说明|示例|
|:---:|:---:|:---:|
|SITE_NAME|	[必填] 网站名称|	小康博客|
|SITE_URL|	[必填] 网站地址，最后不要加 /	|https://www.antmoe.com|
|SMTP_USER|	[必填] SMTP 服务用户名，一般为邮箱地址。	|admin@antmoe.com|
|SMTP_PASS|	[必填] SMTP 密码，一般为授权码，而不是邮箱的登陆密码，请自行查询对应邮件服务商的获取方式	|123|
|SMTP_SERVICE|	[新版支持] 邮件服务提供商，内置支持	|163|
|SENDER_NAME|	[必填] 寄件人名称。	|小康博客|
|TO_EMAIL|	[可选] 博主通知收件地址，默认使用 SMTP_USER	|admin@antmoe.com|
|BLOGGER_EMAIL|	[可选] 如果设置则作为后台管理员邮箱（/sign-up 页面设置），不设置则默认以 SMTP_USER	|admin@antmoe.com|
|TEMPLATE_NAME|	[必填] 设置提醒邮件的主题	|custom2|
|AKISMET_KEY|	[可选] Akismet Key 用于垃圾评论检测，设为 MANUAL_REVIEW 开启人工审核，留空不使用反垃圾	|xxxx|
|ADMIN_URL|	[可选] 后台管理地址 (非博客地址)|	https://xxxx.leanapp.cn/|
|COMMENT|	[可选] 评论 div 的 ID 名	|#vcomment|
|SCKEY	[可选]| server 酱的 SCKEY	|xxx|
|AKISMET_KEY|	[可选] Akismet Key 用于垃圾评论检测	|xxxxxxxxxxxx|
|QMSG_KEY|	[可选] Qmsg 酱的密钥	|xxxxx|
|QQ|	[可选] Qmsg 酱发送的 qq，不填为全部。支持多个，用英文逗号分隔即可	|535668586|
|DISABLE_EMAIL|	[可选]，填写则代表停止发送邮件	|true|
|QQ_SHAKE|	[可选]，填写代表发送 QQ 戳一戳	|true|
|ICP|	[可选] 备案信息，直接填写即可。	|京 ICP 备 19022312 号|
|INFO|	[可选] 自定义信息输出，支持 HTML 代码	|<p style='color:red'>test<p>|
|favicon|	[可选] 网页 favicon 图标	|https://cdn.jsdelivr.net/gh/sviptzk/StaticFile_HEXO/butterfly/img/favicon.ico|
|SPAM_WORDS|	[可选] 需要对屏蔽的关键词，关键词用半角逗号分隔	|单号，物流|
|MAIN_COLOR|	[可选] 仅针对 custom2 模板主题的主要颜色	|#ff9191|
|MAIN_IMG|	[可选] 仅针对 custom2 模板主题的头图	|https://bing.rthe.net/wallpaper|


邮件主题模板一览

|主题|	说明|
|:---:|:---:|
|default|默认主题|
|rainbow|原版的 rainbow|
|custom1|基于🎉梨花町の肾兄さん🎉的模板|
|custom2|对 custom1 的改进版|


填写完成，valine评论配置没有问题，就可以在hexo-server测试一下是否成功，随便发一条评论，查看邮箱是否收到（qq邮箱需要开放授权码，具体方法百度），如果没有问题进入下一步，配置qmsg酱（qq提醒）、server 酱（微信提醒）

1. 申请Qmsg酱
  * 打开官网[Qmsg酱](https://qmsg.zendee.cn/),点击登录，qq登录。
  * 选择qmsg小姐姐
  * 添加接收消息的qq号
  * 加qmsg小姐姐为好友
  * 点击右上角文档，在接口地址url中提取密钥，从'send'到'.html'之间的字母数字组合字符串，这就是qmsg的密钥，保存到环境变量对应的字段中
2. 申请server酱
 * 打开官网[server酱](http://sc.ftqq.com/3.version),开启微信提醒并获取 SCKEY,官网有详细的引导，就不在这里啰嗦了。
最后测试一下，能接收到消息就大功告成，如果有报错，就根据日志分析，解决问题。

## 关于algolia搜索插件
首先需要获取 Algolia官网注册获得了applicationID和apiKey，创建索引库
然后记住IndexName，回到博客文件夹，在博客根目录的_config.yml配置文件中，解开'#'注释，填写appid，appeky，indexName，
在打开butterfly的配置文件（config.yml），将algolia.enable改为true，localserach.enable改为true。
测试搜索是否成功

## 参考Sakura主题，添加了一套鼠标样式css

## daovioce即时聊天工具
* 打开[官网](http://www.daovoice.io/),创建一个免费账户，获取apikey，粘贴到butterfly下配置文件daovoice.adminapikey，enable：改为true
* 测试