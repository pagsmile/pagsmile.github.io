# 订单查询接口

>## 接口链接

    测试URL地址: https://paychanneldev.pagsmile.com/api/checkorder
    正式URL地址: https://paychannel.pagsmile.com/api/checkorder

>## 请求方式

     POST

>## 数据格式   

    请求返回都为JSON    

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
trade_no/out_trade_no | String | Yes | 255 | 请求退款的pagsmile订单号 或 商户自定订单号 | 2018022604263906847
sign | String | Yes | 32 | 签名 |


>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 成功:200
info | String | Yes | 128 | 返回信息 | 成功: SUCCESSFUL
data.merchant_no | String | Yes | 50 | pagsmile分配给商户的ID   
data.app_id | String | Yes | 50 | pagsmile分配给商户的应用ID
data.callback_status | String | Yes | 50 |  订单回调是否成功
data.order_currency | String | Yes | 50 |   订单币种  
data.out_uid | String | Yes | 50 |     用户标示如用户id
data.order_amount | String | Yes | 50 |  订单金额
data.trade_status | String | Yes | 50 |  订单状态
data.trade_no | String | Yes | 50 |  pagsmile交易流水号

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
