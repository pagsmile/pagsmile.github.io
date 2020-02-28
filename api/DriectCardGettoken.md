# 直连信用PCI获取交易安全码token

>## 接口链接

    测试URL地址: https://paychanneldev.pagsmile.com/api/getcardtoken
    正式URL地址: https://paychannel.pagsmile.com/api/getcardtoken
    
>## 请求方式

     POST

>## 数据格式   
  
    json    

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
card_number | String | Yes | 20 | 信用卡卡号 | 4235647728025682
security_code | String | Yes | 4 | 信用卡安全码 | 123
expiration_month | String | Yes | 2 | 信用卡过期月份 | 2022
expiration_year | String | Yes | 2 | 信用卡过期年份 | 12
cardholder_name | String | Yes | 100 | 信用卡持卡人姓名| APRO
sign | String | Yes | 32 | 签名 | 

提示：token有效时间7天，需要提供PCI证书。没有风险控制措施。

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | int | Yes | 10 | 返回状态码 |  200成功
info | string | Yes | 255 | 返回信息 |  102.39
info.token | string | Yes | 32 | 返回支付token值    | 2608f4508569a3461ddb8277844e8e62
info.card_info.first_six_digits | string | Yes | 6 | 返回信用卡前6位数字    | 423564
info.card_info.last_four_digits | string | Yes | 4 | 返回信用卡后4位数字  | 5682
info.card_info.expiration_month | int | Yes | 2 | 返回信用卡过期月份    | 12
info.card_info.expiration_year | int | Yes | 2 | 返回信用卡过期年份    | 2022
info.card_info.cardholder_name | string | Yes | 100 | 返回信用卡持卡人姓名    | APRO
info.card_info.payment_method_id | string | NO | 10 | 返回信用卡持卡卡类型   | 实际卡为准

>## 返回样例

```
  
  {
    "code":"200",
    "info":
        {
            "token":"2608f4508569a3461ddb8277844e8e62",
            "card_info":
                {
                    "first_six_digits":"423564",
                    "last_four_digits":"5682",
                    "expiration_month":12,
                    "expiration_year":2022,
                    "cardholder_name":"APRO"
                    "payment_method_id":"visa"
                }
        }
  }

``` 


>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | 包类型不正确 | 检查参数设置。
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
508 | MERCHANT_STATUS_ISLOCK | 商户状态不可用 | 检查参数中的商户号是否正确或尝试联系客服。
759 | EMAIL_ISNULL | 请求email为空 | 检查参数设置。

更详细列表请参照[返回状态和错误一览](ReturnResult)

>## 签名生成算法  

参考[签名算法](DriectSign)

>## 获取token后请参考直连信用卡支付PCI验证接口

参考直[直连信用卡支付PCI验证接口](DriectPCICreditCard)
