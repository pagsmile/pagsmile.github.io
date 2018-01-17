# 集成式接口

>## 流程示意

![](/assets/img/CreateOrderFlow01.png)

>## 接口链接
    URL地址：https://pserver.pagsmile.com/gateway.json

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
method | String | No | 11 | 支付渠道ID | 103001
out_order_no | String | Yes | 64 | 商户订单号 | 
out_uid | String | Yes | 255 | 商户的用户ID | 
subject | String | No | 255 | 订单标题 |
content | String | No | 255 | 订单内容 |
order_amount | String | Yes | 10 | 订单总金额，精确到小数点后两位。 | 88.88
currency | String | Yes | 3 | 币种 | BRL、USD、EUR
email | String | No | 255 | 邮箱地址 |  
cpf_no | String | No | 64 | CPF号码 | 商城商户此处为必填项；游戏商户选填。
username | String | No | 255 | 用户姓名 | 商城商户此处为必填项；游戏商户选填。
charset | String | Yes | 10 | 请求使用的编码格式，如utf-8,gbk,gb2312等 | utf-8
timestamp | String | Yes | 19 | 发送请求的时间，格式"yyyy-MM-dd HH:mm:ss" | 2018-01-08 15:27:26
version | String | Yes | 10 | 调用的接口版本，固定为：1.0 | 1.0
timeout_express | String | Yes | 255 | 订单有效期 | 1d；1m；1h；1s
passback_params | No | Yes | 255 | 请求回传参数 | 
notify_url | String | No | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com/openapi/notify.json
return_url | String | No | 255 | 服务器同步返回的页面http/https路径。 | https://www.pagsmile.com/success.html
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

>## 返回结果
  请求异常时不进行页面跳转，返回错误状态。

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 
info | String | Yes | 128 | 返回信息 | 

>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
551 | IP_REQUEST_TOO_FAST_LIMIT | 单个IP请求过于频繁 | 查看是否存在恶意刷单
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
403 | SIGN_ISNULL | 未签名 | 检查参数中的签名字段是否正确设置。
405 | SIGN_TYPE_ISNULL | 签名类型未设置 | 检查参数设置。
803 | TRADE_CURRENCY_ISNULL | 币种信息未设置 | 检查参数设置。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
507 | MERCHANT_ID_NOT_ACTIVE | 商户号未激活 | 联系客服查看未激活原因。
602 | APP_ID_INVALID | APP号不可用 | 检查参数中的APP号是否正确。
752 | CPF_NO_ISNULL | 请求CPF号码为空 | 检查参数设置。
924 | CPF_INFO_NOT_MATCH | CPF信息不匹配 | 
512 | MERCHANT_TRADE_NO_ISNULL | 商户订单号为空 | 检查参数设置。
806 | TRADE_TIMEOUT_CLOSE | 该订单已经超过指定过期时效 | 检查参数设置或确认订单信息。
400 | SYSTEM_ERROR | 订单创建失败 | 请尝试重新下单。
550 | SINGLE_DAY_PAY_LIMIT | 超过单日限额 | 检查参数设置或确认订单信息。


>## 签名生成算法  

1. 设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（key1=value1&key2=value2…）拼接成字符串tempData。
     - 如果参数的值为空不参与签名；
     - 参数名区分大小写；

2. 在tempData最后拼接上key得到signData字符串，并signData进行MD5运算，得到sign值signValue。
    - key设置路径：商户平台(paccess.pagsmile.com)
