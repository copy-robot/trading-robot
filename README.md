# trading-robot
一个用Go编写的现代加密货币交易机器人。自行部署，无需第三方依赖。
This is a trading robot that can be used to automate trading on various exchanges.

[![Telegram Global](https://img.shields.io/badge/telegram-global-blue.svg)](https://t.me/+SWTypVxPsQc2MWQ1)

## 配置

添加您的 dotenv 文件：

```sh
Name: trading // 项目名称
Host: 0.0.0.0
Port: 8888 //服务端口

Bitget:
  - Id: 1//自定义编号,必须有
    ApiKey: "<ApiKey>"          //bitget api key
    SecretKey: "<SecretKey>"    //bitget secret key
    Passphrase: "<Passphrase>"  //bitget passphrase
    IsTrader: 2                 //是否开启交易 1 是交易员 2，普通用户
    Mode: 2                     //跟随模式 1 按比跟随 2 按金额跟随
    Proportion: 0.5             //跟随比例
    Amount: 100                 //跟随金额，名义价值

Tradingview:                    //对接tradingview webhook 安全配置，请勿泄露
  TradeUserId: "<TradeUserId>"  //自定义Id 如： "f581eef1fc67d0f3a8a000184edb7359
  SecretKey: "<SecretKey>"      //自定义secret key 如： "66438f1e4cd1438485b98bd5f691e6f7"

TradeUser:                     //okx交易员信息
  - Id: "F6120D38A1EFE6CB"     //自定义Id 如： "F6120D38A1EFE6CB"
    Name: "神鬼军师"            //自定义名称 如： "神鬼军师"
```

    
## Linux环境下运行程序
```
/opt/src/along/TradingRobot  -f  /opt/src/along/etc/trading.yaml
```

## Windows环境下运行程序
```
.\TradingRobot.exe  -f  .\etc\trading.yaml
```

## 推荐使用宝塔Server搭建服务

宝塔Server是一款面向Linux用户的Web面板，可以方便的管理各种服务，包括本项目。

- 下载宝塔面板：[https://www.bt.cn/download.html](https://www.bt.cn/download.html)
- 安装宝塔面板：[https://www.bt.cn/install.html](https://www.bt.cn/install.html)
- 注册并登录宝塔面板：[https://www.bt.cn/register.html](https://www.bt.cn/register.html)
- 导入本项目：[https://www.bt.cn/console/app/import.html](https://www.bt.cn/console/app/import.html)
- 配置宝塔面板：[https://www.bt.cn/console/server/index.html](https://www.bt.cn/console/server/index.html)
- 配置环境变量：在宝塔面板的网站管理面板中，点击网站名称，选择环境变量，添加以下环境变量：
```
Name: trading
Host: 0.0.0.0
Port: 8888
```
- 保存并应用环境变量。
- 启动服务：在宝塔面板的网站管理面板中，点击网站名称，点击启动按钮，启动服务。


## 配置Nginx
```
server {
    listen       80;
    server_name  trading.example.com;

    location / {
        proxy_pass http://127.0.0.1:8888;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

## Tradingview Webhook

```
URL: https://服务器ip:端口/api/order/create 或者 https://trading.example.com/api/order/create

{
    "traderUserId": "f581eef1fc67d0f3a8a000184edb7359",
    "secretKey": "66438f1e4cd1438485b98bd5f691e6f7",
    "id":"{{id}}"
    "symbol": "{{syminfo.basecurrency}}",
    "side": "{{strategy.order.action}}",
    "posSide": "{{strategy.market_position}}",
    "ticker": "{{ticker}}",
    "exchange": "{{exchange}}",
    "close": "{{close}}",
    "open": "{{open}}",
    "high": "{{high}}",
    "low": "{{low}}",
    "time": "{{time}}",
    "volume": "{{volume}}",
    "timenow": "{{timenow}}",
    "interval": "{{interval}}",
    "position_size": "{{strategy.position_size}}",
    "contracts": "{{strategy.order.contracts}}",
    "price": "{{strategy.order.price}}",
    "market_position_size": "{{strategy.market_position_size}}",
    "prev_market_position": "{{strategy.prev_market_position}}",
    "prev_market_position_size":"{{strategy.prev_market_position_size}}"
}
```

## 注意事项
- 本程序只支持bitget交易所的api key，其他交易不支持。
- 本程序只支持邀请注册的bitget账号。邀请链接: [bitget邀请链接](https://partner.bitget.fit/bg/SFK4GR)

## 程序唯一客服 

[![Telegram Global](https://img.shields.io/badge/telegram-global-blue.svg)](https://t.me/+SWTypVxPsQc2MWQ1)