# Payout Apply 接口说明

>## 接口链接

    测试URL地址: https://paychanneldev.pagsmile.com/api/payoutapply
    正式URL地址: https://paychannel.pagsmile.com/api/payoutapply
    
>## 请求方式

     POST

>## 数据格式   
  
    json    

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
email | String | Yes | 255 | 请求转账的邮箱
name | String | Yes | 255 | 转账人姓名
phone | String | Yes | 11 | 转账电话
cpf_no | String | Yes | 11 | 转账人cpf号
amount | Float | Yes | 255 | 请求转账金额
currency | String | Yes | 3 | 请求金额币种 | BRL
bank_id | String | Yes | 10 | 转账人银行编号（参考[巴西银行支付列表](Bankinfo)）
agency | String | Yes | 6 | 转账人支行代码
account_no | Int | Yes | 20 | 转账人银行账号
account_type | String | Yes | 1 | 转账人银行账号类型 0 savings_account 1 checking_account
notify_url | String | 255 | 20 |  转账结果通知地址 | https://www.pagsmile.com
sign | String | Yes | 32 | 签名 | 



>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 200:请求成功
info.trade_no | String | Yes | 128 | 成功返回转账流水号 |  2019080904564629463
data | String | Yes | 256 | 当前状态描述 |  SYSTEM_PARAM_ERROR

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
