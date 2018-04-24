# 直连信用卡退款接口


>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com:8443/api/refund
    正式URL地址：https://paychannel.pagsmile.com/api/refund 
    
>## 请求方式

     POST

>## 数据格式   
  
    json
    
>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
method   | String | Yes | 10 | 渠道代码（默认101001） | 101001 
trade_no | String | Yes | 19 | 平台交易订单号 | 2018042311015505011
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法

    

>## 返回结果

  请求成功后，返回数据在info中。返回的数据按照json格式返回。

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 (成功为200)| 200
info | String | Yes | 128 | 返回订单状态 | REFUND_SUCCESSFUL

>## 成功样例

```
    { 
    "code":"200",
    "info": "REFUND SUCCESSFUL"
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



>## 签名生成算法  

参考[直连签名算法](DriectSign)

>## 启用授权链接

参考[启用授权链接](AuthenticateUrl)
