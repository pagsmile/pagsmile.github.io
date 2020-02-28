# 直连信用卡支付PCI验证接口


>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com/api/creditpci
    正式URL地址：https://paychannel.pagsmile.com/api/creditdopci 
    
>## 请求方式

     POST

>## 数据格式   
  
    JSON
    
>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
payment.out_order_no | String | Yes | 64 | 商户订单号 |
payment.order_amount | String | Yes | 10 | 订单总金额，精确到小数点后两位。金额范围（5-14000） BRL| 88.88
payment.currency | String | Yes | 3 | 币种 | BRL 
payment.subject | String | Yes | 255 | 订单标题 |
payment.content | String | Yes | 255 | 订单内容 |
payment.token | String | Yes | 255 | 信用卡支付凭据（有效期7天） |
payment.installments | String | Yes | 12 | 信用卡分期期数 | 1 不分期 最大12分期
payment.payment_method_id | String | Yes | 16 | 信用卡支发卡组织 |
payment.notify_url | String | Yes | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | 商户的用户ID |  
customer.email | String | Yes | 255 | 邮箱地址 |  
customer.identification | String | Yes(NO) | 64 | 用户信息标示 | 当币种是BRL是必须
customer.identification.type | String | Yes | 50 | 用户信息类型 |  CPF
customer.identification.number | String | Yes | 50 | 用户信息id |  50284414727
customer.username | String | Yes | 255 | 用户姓名 | 用户信息
customer.buyer_ip | String | NO | 255 | 商户的用户ipv4地址 | 
customer.browser | String | NO | 255 | 商户的用户浏览器类型|
customer.phone | String | NO | 255 | 商户的用户的电话|
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名说明

 
 >## 签名说明
     
     设所有发送或者接收到的数据为集合M，如果集合内有多维数组则先进行将维得到一维集合后，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（key1=value1&key2=value2…）拼接成字符串tempData。
          - 如果参数的值为空不参与签名；
          - 参数名区分大小写；
     在tempData最后拼接上key得到signData字符串，并signData进行MD5运算，得到sign值signValue。
 
 >## key的获取
 
 key设置路径：商户平台(paccess.pagsmile.com)
     
 具体设置方式请参照 [签名参数获取方法](/docs/接口参数获取方法.pdf)  
 
 >## 签名样例
     
 1. 将一个多位数组进行降维。降维前数组如下
     
     ```
      [
          'merchant_no' => '102320170519',
          'app_id' => '2017051914172236111',
          'sign_type' => 'md5',
          'payment' => [
              'out_order_no' => 'test-003630',
              'order_amount' => 2000,
              'currency' => 'BRL',
              'subject' => 'test-subject',
              'content' => 'test-content',
              'payment_method_id' => 'visa',
              'installments' => 3,
              'token' => '65800b24cb695abc9e1fca12a65d7106',
              'notify_url' => 'https://www.pagsmile.com',
          ],
          'customer' => [
              'username' => 'APRO',
              'buyer_ip' => '127.0.0.1',
              'browser' => 'safari',
              'email' => 'kongdexin@xcloudgame.com',
              'cpf_no' => '50284414727',
              'out_uid' => 'out_uid',
              'phone' => '11941523675',
              'identification' => [
                          'type' => 'CPF',
                          'number' => '50284414727',
                      ],
          ],
      ]
     
     ```
 2. 数组降维就是将二维数组都降成一维数组，之前是数组的变成一个JSON串，并将该一维数组按照key排序如下
 
     ```
         [
             'app_id' => '2017051914172236111',
             'customer' => '{"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@xcloudgame.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}',
             'merchant_no' => '102320170519',
             'payment' => '{"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com"}',
             'sign_type' => 'md5',
         ]
         
     ```
 
 3. 按照数组按照键值对拼接，并使用'&'链接，在字符串最后拼接上在商户后台得到对密钥key
  
     ```
         app_id=2017051914172236111&customer={"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@xcloudgame.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}&merchant_no=102320170519&payment={"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com"}&sign_type=md5&key=MD5Key
     
     ```
     
 4. 最后将字符串用md5加密得到最后的sign
   
     ```
     67073edadf3c554d0bf17555b0cd9e62
         
     ```

>## 信用卡请求样例

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003169",
                    "order_amount":1000,
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",
                    "paymentMethodId":"visa",
                    "installments":3,
                    "token":"ce0559644ebe1251fa036ff95ea790d6",
                    "notify_url":"https:\/\/www.pagsmile.com"
                   },
        "customer":{
                      "username":"APRO",
                      "buyer_ip":"127.0.0.1",
                      "browser":"safari",
                      "email":"kongdexin@xcloudgame.com",
                      "out_uid":"out_uid",
                      "phone":"11941523675",
                      "identification":{
                                    "type":"CPF",
                                    "number":"50284414727"
                                       }
                       }    
    }
    
 ``` 

>## 返回结果

  请求成功后。返回的数据按照json格式返回。

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 
info.trade_no | String | Yes | 128 | 平台订单号 | 2017042311015505011
info.out_order_no | String | Yes | 128 | 商户订单号| test-003192
info.total_amount | float | Yes | 10 | 订单金额 | 10
info.currency | String | Yes | 10 | 币种 | 
info.trade_status | String | Yes | 10 | 订单状态 | TRADE_SUCCESS

>## 成功样例

```
    {
    "code":"200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","trade_status":"TRADE_SUCCESS"}
    }
    
```
    trade_status 有三个状态 TRADE_SUCCESS 成功  TRADE_REFUSED 支付被银行拒绝 TRADE_RISK_CONTROL 支付在审核中2小时到2天审核
    
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



