# 风控CPF邮箱校验绑定接口说明

>## 接口链接

   测试URL地址：https://paychanneldev.pagsmile.com:8443/api/mailcheck  
   正式URL地址：https://paychannel.pagsmile.com/api/mailcheck 

>## 请求方式

     POST

>## 数据格式   
  
    json
    
>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
cpf_no | String | Yes | 11 | 请求校验的CPF号码，不带特殊符号 | 50284414727 
username | String | Yes | 255 | 请求校验的姓名 | Test User Name
email | String | Yes | 255 | 请求校验的邮箱
return_url | String | No | 255 | 用户在邮箱点击验证成功后的跳转链接 | https://www.pagsmile.com
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

说明：用户邮箱的链接验证时间为1小时，1小时后该链接失效需要重新请求。用的信息cpf和姓名必须是真是有效。一对cpf和姓名可以和多个邮箱绑定，用在邮箱点击验证链接后
会在pagsmile绑定邮箱，成功后会跳转到商户提供的链接，不填写将停留在pagsmile成功绑定页面。

测试：在测试环境使用cpf和姓名对应为 50284414727 和 Test User Name

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 200:成功
info | String | Yes | 128 | 返回信息 | 

>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
200 | SEND EMAIL SUCCESSFUL | 邮件发送成功 |
407 | SEND EMAIL FALSE  | 邮件发送失败
408 | ALREADY VERIFIED  | 该邮件已经与用户名和CPF绑定
401 | SYSTEM_PARAM_ERROR | 包类型不正确 | 检查参数设置。
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
752 | CPF_NO_ISNULL | 请求CPF号码为空 | 检查参数设置。
759 | EMAIL_ISNULL | 请求email为空 | 检查参数设置。
924 | CPF_INFO_NOT_MATCH | CPF信息不匹配 | 
930 | USERNAME_ISNULL | 请求用户姓名为空 | 检查参数设置。

>## 签名生成算法  

参考直[连签名算法](DriectSign)
