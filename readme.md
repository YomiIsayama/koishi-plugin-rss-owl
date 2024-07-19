# koishi-plugin-rss-owl

[![npm](https://img.shields.io/npm/v/koishi-plugin-rss-owl?style=flat-square)](https://www.npmjs.com/package/koishi-plugin-rss-owl)

rss-owl 是一个基于[koishi](https://koishi.chat/manual/starter/)的RSS订阅工具

## 使用方法

### 1. 基本使用
```
rsso 需要订阅的链接或链接组
//如:

//微信公众号话题tag 看理想|李想主义 
rsso https://hub.slarker.me/wechat/mp/msgalbum/MzA3MDM3NjE5NQ==/1375870284640911361
//豆瓣小组-可爱事物分享
rsso https://rsshub.rssforever.com/douban/group/648102
//(以下链接可能需要配置proxy才能显示完整内容)
//telegram每日沙雕墙
rsso https://rsshub.rssforever.com/telegram/channel/woshadiao
//阮一峰的网络日志
rsso http://feeds.feedburner.com/ruanyifeng

//链接组可以将多个链接的推送合并，方便管理
rsso <url1>|<url2>|<url3>...
```
你可以在[RSSHub](https://docs.rsshub.app/zh/routes/popular)中找到需要的链接

并在[RSSHub公共实例](https://docs.rsshub.app/zh/guide/instances)中寻找替换可用的实例

当然，自己部署也是可以的

### 2. 参数说明
```
// arg 可以写入局部参数，这会在获取该订阅时覆盖掉插件配置，允许修改绝大部分配置中的参数，但要注意，参数内不能使用`,`和`:`，否则会造成解析错误
// 关闭代理，并使用custom
// 需要注意的是，videoRepost和toHTML在此仅可关闭而不能打开，你只能在插件配置中打开
rsso -a proxyAgent:false,rssItem:custom <url>

//添加代理时不能有:号
rsso -a proxyAgent:http//127.0.0.1/7890,auth:username/password <url>

//forceLength和refresh的组合可以让你订阅一些不提供更新时间的订阅，如排行榜
rsso -a forceLength:10,refresh:1440 <url>

//custom和domFrame都可以修改该订阅的外观，使用`&nbsp;`代替空格以避免koishi解析错误
rsso -a custom:<div&nbsp;style='width:600px'>{{description}}</div> <url>
```

```
// rss-item 与arg不同的是，在此你可以使用`:`来定义解析规则，第一位必须是rss的key或者custom，第二位是可选的content，第三位是可选的merge来使用合并消息
rsso -i custom,description:text:merge <url>

// keyword-filter 关键字过滤，会与配置中的进行合并
rsso -k nsfw,something <url>

// content [default|html|text|image|video|proto]
// 提取规则,default会优先使用html,关闭html时会将文字和图片分开发送,text|image|video仅会发送相关的内容,proto会将rss推送不做任何处理发送
rsso -c html <url>

// title
自定义名称，一般配合链接组进行使用
rsso -t 订阅名称 <url>

// force 
// 强行写入而不仅过验证，因此，订阅时最后一次更新不会被推送

// test
测试链接，不会写入订阅
rsso -T <url>

// daily
指定该订阅每天更新时间和更新条数
//refresh:1440,forceLength:10
rsso -d 8:00/10 <url>
//refresh:1440
rsso -d 8:00 <url>

rsso -a reverse:true -d 8:00/10 <url>

```

## 致谢:

- [koishi-plugin-rss](https://github.com/koishijs/koishi-plugin-rss)
- [koishi-plugin-rss-discourse](https://github.com/MirrorCY/koishi-plugin-rss)
- [koishi-plugin-rss-cat](https://github.com/jexjws/koishi-plugin-rss-cat)