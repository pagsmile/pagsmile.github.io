# Credit Card Payment Verification Interface

>## Flow

>## Interface URL

    Test Environment：https://paychanneldev.pagsmile.com/api/creditdo
    Prod Environment：https://paychannel.pagsmile.com/api/creditdo 
    
>## Method

     POST

>## Data Format   
  
    json
    
>## Request Parameters

Param | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | Merchant ID created by pagsmile | 1024201708140012289
app_id | String | Yes | 20 | APP ID created by pagsmile | 2017051914172236111
sign_type | String | Yes | 10 | MD5 only | MD5
payment.out_order_no | String | Yes | 64 | merchant trade reference |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Amount range (5-14000) BRL| 88.88
payment.currency | String | Yes | 3 | currency | BRL 
payment.subject | String | No | 255 | subject |
payment.content | String | No | 255 | content |
payment.token | String | Yes | 255 | Credit card payment credentials (valid for 7 days) |
payment.installments | String | Yes | 12 | Credit card installment period | 1 no staging, maximum 12 staging
payment.paymentMethodId | String | Yes | 16 | Credit card issuing card organization |
payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | user id from merchant |  
customer.email | String | Yes | 255 | email |  
customer.cpf_no | String | Yes | 64 | CPF | 
customer.username | String | Yes | 255 | user name | 
customer.buyer_ip | String | NO | 255 | IP address from merchant user | 
customer.browser | String | NO | 255 | browser type from merchant user |
customer.phone | String | NO | 255 | phone from merchant user|
sign | String | Yes | 32 | sign string | The signature value calculated by the signature algorithm is detailed in the signature generation algorithm.

     Note: The boleto currency currently only supports USD and BRL. The cpf and username used in the test environment are 50284414727 and Test User Name.
     

>## Sample

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "currency":"BRL",
                    "paymentMethodId":"visa",
                    "token"："67a9449686cf8f57dc28cbc88ad82245",
                    "subject":"test-subject",
                    "content":"test-content",
                    "notify_url":"https://www.pagsmile.com"
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",
                    "cpf_no":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"11941523675"
                    },
               
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## Return Result

  After the request is successful. The returned data is returned in json format.

Param | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | 
info.trade_no | String | Yes | 128 | pagsmile trade NO. | 2017042311015505011
info.out_order_no | String | Yes | 128 | merchant trade reference| test-003192
info.total_amount | float | Yes | 10 | order amount | 10
info.currency | String | Yes | 10 | currency | 
info.trade_status | String | Yes | 10 | status | TRADE_SUCCESS

>## Success Sample

```
    {
    "code":"200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","trade_status":"TRADE_SUCCESS"}
    }

>## Fail Sample

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```

>## Error Code

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature generation algorithm

Reference straight [continuous signature algorithm](SignatureAlgorithm)

