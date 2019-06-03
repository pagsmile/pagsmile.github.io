# 直连现金闪付接口

>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com/api/flashpay
    正式URL地址：https://paychannel.pagsmile.com/api/flashpay 
    
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
payment.method   | String | Yes | 10 | 渠道代码（默认） | 110010 
payment.subject | String | No | 255 | 订单标题 |
payment.content | String | No | 255 | 订单内容 |
payment.bank | String | Yes | 255 | 支付银行 |tau,santander,bradesco,banco-do-brasil
payment.notify_url | String | Yes | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com
customer.out_uid | String | No | 255 | 商户的用户ID |  
customer.email | String | Yes | 255 | 邮箱地址 |  
customer.cpf_no | String | Yes | 64 | CPF号码 | 
customer.username | String | Yes | 255 | 用户姓名 | 
customer.buyer_ip | String | No | 255 | 商户的用户ipv4地址 | 
customer.browser | String | No | 255 | 商户的用户浏览器类型|
customer.phone | String | Yes | 9 | 商户的用户的电话，8位或9位数字| 
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

     说明：币种目前只支持USD和BRL，在测试环境中使用的
     
        cpf_no 和username是50284414727和Test User Name
    
     支付银行参数目前支持四个银行分别是itau,santander,bradesco,banco-do-brasil 
     
   
     

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
                    "method":"106001",
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",  
                    "bank":"itau",            
                    "notify_url":"www.pagsmile.com",  
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",
                    "cpf_no":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"941523675"
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
info.trade_no | String | Yes | 128 | 平台订单号 | 2017042311015505011
info.out_order_no | String | Yes | 128 | 商户订单号| test-003192
info.total_amount | float | Yes | 10 | 订单金额 | 10
info.bank_name | String | Yes | 10 |  付款对公账户名银行名称 | 
info.account_owner | String | Yes | 50 | 付款对公账户名称 | 
info.account_owner_document | String | Yes | 10 | 付款对公账户账户cpf号 | 
info.account_agency | String | Yes | 10 | 银行分行号 | 
info.account_number | String | Yes | 10 | 银行账号 | 
info.bank_logo | String | Yes | 10 | 银行logo | 
info.check_url | String | Yes | 10 | 支付凭证验证链接 |


>## 成功样例

```
    { 
    "code":"200",
    "info":{"code":"200","info":{"trade_no":"2018070909341506645","currency":"USD","amount":100,"bank_name":itau,"out_order_no":"test-0011531140105503","account_owner":"Agillitas Solu","account_owner_document":"13.776.742\/0001-55","account_agency":"0910","account_number":"05841-1","bank_logo":"https:\/\/d2g83ydku1zde9.cloudfront.net\/pagsmile\/Itau-logo.png","check_url":"http:\/\/bit.ly\/2NFMlMK"}
    
```

>## 失败样例

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```  

>## 状态流程示意

![](/assets/img/status_flow_levpay&lottery.jpg)


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
760 | PHONE_ISNULL | 请求电话号码为空 | 检查参数设置。
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
