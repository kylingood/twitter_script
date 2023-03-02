# 功能

twitter
- 关注（follow）
- 点赞（like）
- 转推（retweet）
- 评论（reply）
- 根据条件随机选择推文，点赞转推评论
- 随机选择一个互关贴，转推关注（作者及评论者）
- 回关

指纹浏览器
- 批量创建浏览器
- 批量修改代理

# 前置条件
- python3，可通过anaconda安装
- 编辑器，如vscode
- 指纹浏览器，如bitbrowser、adspower
- 独立ip

# 说明
- python、编辑器问题需要自行搜索答案。
- 本程序在mac下测试，windows需要自行测试
- 本程序默认使用比特浏览器。如需使用ads浏览器，twitter_py文件需要如下修改
```
# 导入adspower文件
from browser.adspower import *

# OAuth2ForTwitterUtil类改为继承AdspowerUtil类
class OAuth2ForTwitterUtil(AdspowerUtil):
```

# 准备

## 创建twitter应用程序，设置OAuth2，获取key

twitter开发者平台网址：https://developer.twitter.com/en/portal/dashboard

1、创建项目生成key
![twitter创建项目生成key](https://s2.loli.net/2022/07/13/zslLJa5TkdRmAuG.jpg)

2、设置OAuth2并生成client_id和client_secret(只有机密客户，才需要client_secret)
![twitter设置OAuth2并生成clientID](https://s2.loli.net/2022/07/13/7X1mVTicu8ABIC5.jpg)

## 准备数据文件

完整文件结构
```
twitter_script
    twitter_
        twitter_.py
        refresh_tokens.json
    browser
        bitbrowser.py
        adspower.py
    data
        twitter.csv
        ip.csv
        bitbrowser.xlsx
        adspower.xlsx
        tweet_texts.txt
        reply_texts.txt
    config.py
    README.md
    .gitignore
```

由于数据属于敏感文件，不能上传。需要自行补齐数据文件。xxxxx的地方换成你自己的数据

1、config.py
```
client_id = "xxxxxxxxxx"
client_secret = "xxxxxxxxxx"
redirect_uri = "https://twitter.com/home"

refresh_tokens_file = './twitter_/refresh_tokens.json'
tweet_texts_file = './data/tweet_texts.txt'
reply_texts_file = './data/reply_texts.txt'

# AdsPower Local API 接口
adspower_url = 'http://local.adspower.com:xxxxx'
# BitBrowser Local API 接口
bitbrowser_url = 'http://127.0.0.1:xxxxx'
```

2、refresh_tokens.json

各推特账号的刷新令牌。留空即可，程序会自动更新
```
{}
```

3、twitter.csv

你的twitter账号数据。只列出了username和password。可以自行添加其他字段
```
twitter_username|twitter_password|...
xxxxx|xxxxx|...
xxxxx|xxxxx|...
......
```

4、ip.csv

你的独立ip数据
```
ip:post:account:password
xxxxx:xxxxx:xxxxx:xxxxx
xxxxx:xxxxx:xxxxx:xxxxx
......
```

5、tweet_texts.txt

要发布的推文内容文件。找点鸡汤文之类的，一行一个。调用时程序会随机选择一条发推。
```
Never evade problems, time will not give the weak anything in return.
You can‘t do it — that’s the biggest lie on earth。
......
```

6、reply_texts.txt

要评论的内容文件。搜集点马屁话，一行一个。调用时程序会随机选择一条发评论。
```
good job
great
......
```

7、bitbroswer.xlsx

比特浏览器数据文件。需要创建完浏览器后导出数据文件，并重命名。


# 示例

1. 批量创建指纹浏览器（程序创建没有设置代理）并导出浏览器数据文件
2. 批量修改代理ip
3. 批量授权(会自动打开浏览器。唯一一次需要在浏览器里操作的)
4. 批量处理业务（如批量关注、转推等）
5. 择时重复4

示例详见`bitbrowser.py`、`twitter_py`文件（底部）
