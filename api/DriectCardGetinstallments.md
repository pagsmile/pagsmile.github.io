# 直连信用卡分期期数金额查询

>## 接口链接

    测试URL地址: https://paychanneldev.pagsmile.com/api/getinstallments
    正式URL地址: https://paychannel.pagsmile.com/api/getinstallments
    
>## 请求方式

     POST

>## 数据格式   
  
    json    

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
amount | String | Yes | 20 |  分期查询金额 | 100
sign | String | Yes | 32 | 签名 | 

提示：发送退款请求时，该笔订单必须是成功状态。

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
installments | int | Yes | 10 | 返回期数 |  2
installment_amount | float | Yes | 10 | 返回期数一期金额 |  102.39
total_amount | float | Yes | 10 | 总扣款金额    | 204.78

>## 返回样例

```
 {
 
 "1":{"installments":1,"installment_amount":200,"total_amount":200},
 
 "2":{"installments":2,"installment_amount":102.39,"total_amount":204.78},
 
 "3":{"installments":3,"installment_amount":69.85,"total_amount":209.56},
 
 "4":{"installments":4,"installment_amount":53.59,"total_amount":214.34},
 
 "5":{"installments":5,"installment_amount":43.6,"total_amount":217.98},
 
 "6":{"installments":6,"installment_amount":36.83,"total_amount":220.98},
 
 "7":{"installments":7,"installment_amount":31.95,"total_amount":223.66},
 
 "8":{"installments":8,"installment_amount":28.12,"total_amount":224.98},
 
 "9":{"installments":9,"installment_amount":25.16,"total_amount":226.42},
 
 "10":{"installments":10,"installment_amount":22.92,"total_amount":229.18},
 
 "11":{"installments":11,"installment_amount":21.09,"total_amount":232},
 
 "12":{"installments":12,"installment_amount":19.57,"total_amount":234.82}
 
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
