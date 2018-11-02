# 商户汇率查询

>## 接口链接

    测试URL地址: http://testenv.pagsmile.com/pserver/api/exchange/query.json
    正式URL地址: （未上线）http://pserver.pagsmile.com/api/exchange/query.json
    
>## 请求方式

     GET/POST

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
source | String | Yes | 3 | 源币种 | USD
target | String | Yes | 3 | 目标币种 | BRL
sign | String | Yes | 32 | 签名 | 


>## 返回结果 

参数 | 类型 | 是否必填 | 描述 | 示例值
---  | ---  | ---   | ---  | ---
code | String | Yes | 返回状态码 | 成功:200 
info | String | Yes | 返回信息 | 成功: SUCCESS
data | String | Yes | 汇率值（最多保留4位小数）

>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | 请求参数有误 | 检查参数设置。
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
602 | APP_ID_INVALID | APP状态不可用 | 检查参数中的app_id是否正确或尝试联系客服。

更详细列表请参照[返回状态和错误一览](ReturnResult)

>## 签名生成算法  

参考[签名算法](DriectSign)
