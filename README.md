主要更新：其实也没什么，只是原作者的代码少了一个sleep的设置，导致如果对方换IP的地址没及时反映，那这个脚本就会疯狂发换IP的指令，1秒5次都没问题，然后你就被IDC老板拉黑了。
我的代码中加入了`sleep 5m`意思是5分钟后再检查更新的IP能不能解锁Netflix；如果不能解锁，再发送一次指令。

提示：小白不知道什么是动态IP服务器的就不要用了，动态IP是台湾的hinet，香港的hkt等。其他机器都是静态IP，是换不了IP的。

***

# changip 全自动流媒体解锁监控 猴子修改版
一个可以监控Netflix被锁然后自动换IP的机器；仅对动态ip，通过api换ip的有效。脚本原作者为[yxkumad](https://github.com/yxkumad/streammonkeylite)。
***

# 功能
- 监控可换IP机器的IP是否被Netflix封了
- 如果封了，自动通过主机商提供的api更换ip
- 更换结果通过TG发送通知
- 更换后自动监测，如果还是被封，再次更换。
***

# 如何使用
1.下载脚本

	wget -O changip.sh https://raw.githubusercontent.com/gtgc2005/changip/main/changip.sh && chmod +x changip.sh

2.修改changip.sh

	nano changip.sh

根据提示修改以下内容，其中TG机器人可以不填，但换IP后就不会提醒了
```
# NAME=自己定义，例如HKT,注意保留引号
NAME="HKT"

# API=你更换IP的链接，每家不一样，自己替换，注意保留引号
API="htts://"

# TG_BOT_TOKEN=自行前往@Botfather获取,默认null

TG_BOT_TOKEN=null
# TG_CHATID=与机器人@userinfobot 对话,默认null
TG_CHATID=null
```
3.运行脚本一次

	./changip.sh

4.设为定时任务
输入 `crontab -e` 然后会弹出 vi 编辑界面，按小写字母 i 进入编辑模式，在文件里面添加一行：

	*/10 * * * * /root/changip.sh >/dev/null 2>&1

# TG机器人的申请

* TG_BOT_TOKEN的获取

telegram 中关注官方 @Botfather ，输入/newbot ，创建新的机器人（bot）时，会提供的 token（在提示 Use this token to access the HTTP API:后面一行）创建 bot 后，需要先在 telegram 中与 BOT 进行对话（随便发个消息），然后才可用 API 发送消息。

* TG_CHATID的获取

与机器人@userinfobot 对话可获得。

# 感谢
原作者[yxkumad](https://github.com/yxkumad/streammonkeylite)
