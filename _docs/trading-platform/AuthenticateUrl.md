---
title: AuthenticateUrl
category: 交易平台
order: 15
language: cn
---

# 启用授权链接

### 1. 授权链接说明
    
   用户需要去发卡行登陆授权后才可以执行授权操作
         
   

### 2. 开启授权后

    授权成功后将会返回一个授权跳转链接
    
参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 (成功为200)| 200
info | String | Yes | 128 | 返回的认证链接 | https:\/\/authorizationmocksandbox.cieloecommerce.cielo.com.br\/CardAuthenticator\/Receive\/7984d820-a136-400f-98a4-1db86b9104f5

   说明：测试环境授权链接跳转获取到后，执行跳转操作，在select选择框中，'Autenticado'授权成功，'Não autenticado'授权失败
 

成功得到授权链接样例

```
    { 
    "code":"200",
    "info":"https:\/\/authorizationmocksandbox.cieloecommerce.cielo.com.br\/CardAuthenticator\/Receive\/7984d820-a136-400f-98a4-1db86b9104f5"
    }
    
```

1. 授权成功后，将会向商户提供的授权链接以POST方式发送授权成功的数组

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
status | String | Yes | 16 | 返回状态| 200 | success
trade_no | String | Yes | 128 | 平台订单号 |  2018042311570804284
info | String | Yes | 128 | 返回成功信息 |  success


    
    ```
        {
              ["status"]=>
              string(7) "success"
              ["trade_no"]=>
              string(19) "2018042311570804284"
              ["info"]=>
              string(8) "success "
        }
        
    ```


2. 授权失败后，将会向商户提供的授权链接以POST方式发送授权失败的数组

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
status | String | Yes | 16 | 返回状态| failed | failed
trade_no | String | Yes | 128 | 平台订单号 |  2018042311570804284
info | String | Yes | 128 | 返回失败原因信息 |  bank-91-failed



    ```
        {
               ["status"]=>
               string(7) "failed"
               ["trade_no"]=>
               string(19) "2018042311570804284"
               ["info"]=>
               string(8) "bank-91-failed "
        }
    ```
    
   

