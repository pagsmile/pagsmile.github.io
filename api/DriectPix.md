# 直连PIX接口

>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com/api/pix
    正式URL地址：https://paychannel.pagsmile.com/api/pix 
    
>## 请求方式

     POST

>## 数据格式   
  
    json
    
>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
version | String | Yes | 10 | 调用的接口版本，固定为：1.0 | 1.0
timeout_express | String | Yes | 255 | 订单有效期 | 一天的时间赋值为:1d或者24h或者1440m；
timestamp | String | Yes | 19 | 发送请求的时间单位为秒 | 21516081919
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
payment.out_order_no | String | Yes | 64 | 商户订单号 |
payment.order_amount | String | Yes | 10 | 订单总金额，精确到小数点后两位。金额范围（5-14000） BRL| 88.88
payment.currency | String | Yes | 3 | 币种 | BRL 
payment.subject | String | Yes | 255 | 订单标题 |
payment.content | String | Yes | 255 | 订单内容 |
payment.notify_url | String | Yes | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com
payment.return_url | String | No | 255 | 服务器同步返回的页面http/https路径。 | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | 商户的用户ID |  
customer.email | String | Yes | 255 | 邮箱地址 |  
customer.id_type | String | Yes | 64 | CPF/CNPJ |  
customer.id | String | Yes | 64 | 内容 | CPF/CNPJ 内容
customer.username | String | Yes | 255 | 用户姓名 | 商城商户此处为必填项；游戏商户选填。
customer.phone | String | NO | 255 | 商户的用户的电话|
customer.buyer_ip | String | NO | 255 | 商户的用户ipv4地址 | 
customer.browser | String | NO | 255 | 商户的用户浏览器类型|
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

     说明：pix 币种目前支持BRL 在测试环境中使用的cpf和username是50284414727和Test User Name

>## 请求样例

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",
                    "return_url":"https://www.pagsmile.com",
                    "notify_url":"https://www.pagsmile.com"
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",
                    "id_type":"CPF",
                    "id":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"11941523675"
                    },
                     
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## 返回结果

  请求成功后，可以使用info.qrCode生成二维码。

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 
info.trade_no | String | Yes | 128 | 平台订单号 | 2017042311015505011
info.out_trade_no | String | Yes | 128 | 商户订单号| test-003192
info.total_amount | float | Yes | 10 | 订单金额 | 10
info.currency | String | Yes | 10 | 币种 | 
info.expiration | int | Yes | 10 | 过期时间秒数 | 
info.qrCode | String | Yes | 10 | 二维码数值 | 
info.qrCode_img | String | Yes | 10 | 二维码 |

>## 成功样例

```
    {
        "code":"200",
        "info":
            {
            "trade_no":"2021010603595990948",
            "currency":"BRL",
            "amount":100,
            "out_trade_no":"test-003189",
            "expiration":7200,
            "qrCode":"00020101021126910014BR.GOV.BCB.PIX2569api-pix-h.bancobs2.com.br/spi/v2/a5631b32-8737-4abc-959d-9dface195a6f5204000053039865405100.05802BR5913Pagsmilepixpj6014Belo Horizonte61083038040362070503***63049587",
            "qrCode_img":"https://paychanneldevin.pagsmile.com/api/pixcode?p=EB7E1DBE0CB0FB7853CE561CDA375053E2C2A1E6CDD370E95D95D8"
            }
            
    }
    
```

>## 失败样例

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```


>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
403 | SIGN_ISNULL | 未签名 | 检查参数中的签名字段是否正确设置。
405 | SIGN_TYPE_ISNULL | 签名类型未设置 | 检查参数设置。
803 | TRADE_CURRENCY_ISNULL | 币种信息未设置 | 检查参数设置。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
507 | MERCHANT_ID_NOT_ACTIVE | 商户号未激活 | 联系客服查看未激活原因。
602 | APP_ID_INVALID | APP号不可用 | 检查参数中的APP号是否正确。
752 | CPF_NO_ISNULL | 请求CPF号码为空 | 检查参数设置。
759 | EMAIL_ISNULL | 请求email为空 | 检查参数设置。
924 | CPF_INFO_NOT_MATCH | CPF信息不匹配 | 
930 | USERNAME_ISNULL | 请求用户姓名为空 | 检查参数设置。
512 | MERCHANT_TRADE_NO_ISNULL | 商户订单号为空 | 检查参数设置。
806 | TRADE_TIMEOUT_CLOSE | 该订单已经超过指定过期时效 | 检查参数设置或确认订单信息。
400 | SYSTEM_ERROR | 订单创建失败 | 请尝试重新下单。
550 | SINGLE_DAY_PAY_LIMIT | 超过单日限额 | 检查参数设置或确认订单信息。

更详细列表请参照[返回状态和错误一览](ReturnResult)

>## 签名生成算法  

参考直[连签名算法](DriectSign)

