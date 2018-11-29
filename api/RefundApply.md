# Refund接口说明

>## 接口链接

    测试URL地址: https://paychanneldev.pagsmile.com/api/refundapply
    正式URL地址: https://paychannel.pagsmile.com/api/refundapply
    
>## 请求方式

     POST

>## 数据格式   
  
    json    

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
trade_no | String | Yes | 255 | 请求退款的pagsmile订单号 | 2018022604263906847
email | String | Yes | 255 | 请求退款的邮箱
refund_amount | Float | Yes | 255 | 请求退款金额
description | String | No | 255 | 退款描述
sign | String | Yes | 32 | 签名 | 

提示：发送退款请求时，该笔订单必须是成功状态。

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 200:成功
info | String | Yes | 128 | 返回信息 | SUCCESS
data | String | Yes | 256 | 当前订单状态    |  REFUND_IN_VERIFY（用户信息确认中）/ REFUND_IN_PROCESS（退款处理中）

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
