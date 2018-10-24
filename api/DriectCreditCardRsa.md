# 直连信用卡rsa加密算法接口

>## 流程示意



>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com/apiv2/credit
    正式URL地址：https://paychannel.pagsmile.com/apiv2/credit 
    
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
passback_params | String | Yes | 255 | 透传参数 | 默认passback_params
timestamp | String | Yes | 19 | 发送请求的时间单位为秒 | 21516081919
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
payment.out_order_no | String | Yes | 64 | 商户订单号 |
payment.order_amount | String | Yes | 10 | 订单总金额，精确到小数点后两位。 | 88.88
payment.currency | String | Yes | 3 | 币种 | BRL 
payment.method   | String | Yes | 10 | 渠道代码（默认） | 101001 
payment.subject | String | No | 255 | 订单标题 |
payment.content | String | No | 255 | 订单内容 |
payment.notify_url | String | Yes | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com
payment.return_url | String | No | 255 | 服务器同步返回的页面http/https路径。 | https://www.pagsmile.com
payment.authenticate | int | No | 4 | 是否需要持卡人授权（默认是否） | 0或者1
payment.authenticate_back_url | String | No | 255 | 授权后跳转链接。（当payment.authenticate 为1时必须） | https://www.pagsmile.com
payment.credit_card.number | String | Yse | 19 | 卡号 | 455187******0183 加密传输
payment.credit_card.holder | String | Yse | 255 | 持卡人姓名。 | Test User Name 加密传输
payment.credit_card.expirationDate | String | Yse | 7 | 信用卡逾期时间。 | 12/2030 加密传输
payment.credit_card.securityCode | String | Yse | 4 | 信用卡背面安全码。 | 123 加密传输
payment.credit_card.brand | String | No | 10 | 信用卡发卡行。(visa,master,amex,elo,aura,jcb,dinners,discover) | visa 加密传输
customer.out_uid | String | No | 255 | 商户的用户ID |  
customer.email | String | No | 255 | 邮箱地址 |  
customer.cpf_no | String | Yes | 64 | CPF号码 | 商城商户此处为必填项；游戏商户选填。
customer.username | String | Yes | 255 | 用户姓名 | 商城商户此处为必填项；游戏商户选填。
customer.buyer_ip | String | No | 255 | 商户的用户ipv4地址 | 
customer.browser | String | No | 255 | 商户的用户浏览器类型|
customer.phone | String | No | 255 | 商户的用户的电话|
address.zip_code | String | No | 8-8 | 用户的通讯地址邮政编码| 06233-200
address.street_name | String | No | 70 | 用户的通讯地址街道名称| Av. das Nações Unidas
address.street_number | String | No | 10 | 用户的通讯地址街道编号| 3003
address.neighborhood | String | No | 50 | 用户的通讯地址社区地址| Bonfim
address.city | String | No | 50 | 用户的通讯地址的城市| Osasco
address.federal_unit | String | No | 2 | 用户的通讯地址的州缩写| SP
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

     说明：币种目前只支持USD和BRL，在测试环境中使用的
     
        cpf_no 和username是50284414727和Test User Name
     
     测试卡号，卡类型不限，推荐visa
        
        成功 0000000000000001 或者 0000000000000004
        失败 0000000000000002 或者 0000000000000008
     
     其中rsa加密传输卡信息包括 number holder expirationDate  securityCode brand  
     
>## 请求样例

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "passback_params":"passback_params",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "method":"101001",
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",
                    "return_url":"https://www.pagsmile.com",
                    "notify_url":"https://www.pagsmile.com",
                    "authenticate":0,
                    "authenticate_back_url":"www.pagsmile.com",
                    "credit_card":{
                          "number":"WLoCFvecGC5J+mAk8IgtuLLtF7GKl9FewZZUEHF5SuyejAkjmd4hgiRkQF4LBHC3gPgKjKuYQ+V23adW6aka0ukgvkGQlv1eTHE6xd0JcZ2zOKe6XYiRmUerhY5HvO9QSh7YfB79IAVXx61TCUGYmKBjj1TD+FpRWHv+WCKhkoo=",
                          "holder":"JZi57dOwA8JRbfrqM14Wa6Q/XGWrBSzeMXhYmnxhuHKUr5NDzQymKkOIhuihW/WLnBro6581V3o+uA1TLfnYf2uZg7vohDKSqhWVMpqwM7j5yVgP5sHIvgk3WQAQ9OAJdQN7qHNPdTQnxZKShGBs9ikaRgktBBEOGhCcraosdHY=",
                          "expirationDate":"'BPfrZvTBEgygNlQg6OhXz52jYrD9XgGAzVdsttLcgP5Gh79tH/3fXbYPe4A9cTiNsN/gumRQNUBVgnKerF4HZezceDUb0dnY0YstVqizWfNiGeinRBYSS3irCy5QU190CVDAfdghZrCQXAioLRc6y87irr2xgZHjfQyj2/Q8axA=",
                          "securityCode":"'ILXEUj35AiRjqdOLfzD8EHzenszCMekxXV9IPlRhuDK+0Dm69nofaZRoT1qGYMs08GPGTgoPURnN6SeZqhXhWkqwu7I1jpzNwtg7OfTsnAtQ3jlXB6xIdIbCeP5dCIvCbhYLHU/miMGowcnJfI4kiXiwgklk5Ii3uqY3z9cO6HM=",
                          "brand":"OQCfZJK5ZR366cYHMZpy8b4qk2H4ltX4rmrpB0t4hAoGdlLuu7h8e47zXOnhPYFkoGSIRSiacggw1/PKqK4LOqibbVpdLduvBPuEhj/RQu1wH0OURPFm4H1Yi6ch29uBBN1zOAlQWLMD3W+WzA8jDngOec57bwVtbH2weQUT72Q="
                                         
                    }
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",
                    "cpf_no":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"11941523675"
                    },
        "address":{
                    "zip_code":"06233-200",
                    "street_name":"Av. das Nações Unidas",
                    "street_number":"3003",
                    "neighborhood":"Bonfim",
                    "city":"Osasco",
                    "federal_unit":"SP"
                    },               
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## 返回结果

  请求成功后，返回数据在info中。返回的数据按照json格式返回。

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 (成功为200)| 200
info.trade_status | String | Yes | 128 | 返回订单状态 | TRADE_SUCCESS
info.trade_no | String | Yes | 128 | 平台订单号 | 2017042311015505011
info.out_order_no | String | Yes | 128 | 商户订单号| test-003192
info.total_amount | float | Yes | 10 | 订单金额 | 10
info.currency | String | Yes | 10 | 币种 | 


  如果有授权跳转链接 ,请求成功后，返回在一个post表单中，其中提交地址为authenticate_back_url
  
  参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
  ---  | ---  | ---      | ---      | ---  | ---
  status | String | Yes | 16 | 返回状态码 (成功为success)| success
  trade_no | String | Yes | 16 | 平台订单号 | 2017042311015505011
  info | String | Yes | 16 | 返回状态信息 (成功为success)| success

>## 成功样例

```
    { 
    "code":"200",
    "info":{"trade_status":"TRADE_SUCCESS","trade_no":"2018042311015505011","out_order_no":"test-003192","total_amount":10,"currency":"BRL"}
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
910 | CARD_NO_ISNULL | 卡号为空     | 检查参数
911 | CARD_TYPE_ISNULL | 卡类型为空     | 检查参数
912 | CARD_IS_BLACK_CARD | 卡号被所     | 检查参数
913 | CARD_USER_INFO_NOT_MATCH | 卡信息不符     | 检查参数
914 | CARD_USER_USER_TO_MANY | 绑卡超过上限     | 检查参数
915 | CARD_TRADE_TOO_FREQUENT | 卡交易太频繁     | 检查参数
917 | CARD_TRADE_IP_LIMIT | 卡号IP受限    | 检查参数
922 | CPF_IS_BLACK_CPF | 身份证号被锁定     | 检查参数
923 | CPF_IS_VERIFYING | 身份证好验证中     | 检查参数
924 | CPF_INFO_NOT_MATCH | CPF信息不匹配 | 
930 | USERNAME_ISNULL | 请求用户姓名为空 | 检查参数设置。
512 | MERCHANT_TRADE_NO_ISNULL | 商户订单号为空 | 检查参数设置。
806 | TRADE_TIMEOUT_CLOSE | 该订单已经超过指定过期时效 | 检查参数设置或确认订单信息。
400 | SYSTEM_ERROR | 订单创建失败 | 请尝试重新下单。
550 | SINGLE_DAY_PAY_LIMIT | 超过单日限额 | 检查参数设置或确认订单信息。

更详细列表请参照[返回状态和错误一览](ReturnResult)

>## 签名生成算法  

参考[直连签名算法](DriectSign)

>## RSA数据加密算法  

参考[卡信息RSA签名算法](DriectSignRsa)

>## 启用授权链接

参考[启用授权链接](AuthenticateUrl)
