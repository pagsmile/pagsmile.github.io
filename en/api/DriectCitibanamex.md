# Citibanamex API

>## API URL

    Test Environment : https://paychanneldev.pagsmile.com/api/citibanamex
    Production Environment : https://paychannel.pagsmile.com/api/citibanamex

>## Request Method

     POST

>## Format   

    JSON

>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
version | String | Yes | 10 | API Version, for now is fixed to: 1.0 | 1.0
timeout_express | String | Yes | 255 | Order validity | One-day assignment: 1d or 24h or 1440m;
timestamp | String | Yes | 19 | Request is sending by second | 21516081919
sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
payment.out_order_no | String | Yes | 64 | Merchant order number |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Range: 10-40000 MXN | 88.88
payment.currency | String | Yes | 3 | Currency | MXN
payment.subject | String | Yes | 255 | Order Subject |
payment.content | String | Yes | 255 | Order Content |
payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
payment.return_url | String | No | 255 | The http/https path of the page returned synchronously by the server. | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | Merchant’s user ID |  
customer.email | String | Yes | 255 | email address |  
customer.username | String | Yes | 255 | User Name | Mall merchants are required here; game merchants are optional.
customer.buyer_ip | String | NO | 255 | User’s ipv4 address |
customer.browser | String | NO | 255 | User’s browser type |
customer.phone | String | NO | 255 | User’s Phone number |
sign | String | Yes | 32 | The signature string of the merchant request parameter | The signature value calculated by the signature algorithm is detailed in the signature generation algorithm.

     Note : order amount Range from 10 to 40000 MXN.

>## Request Sample

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "currency":"MXN",
                    "subject":"test-subject",
                    "content":"test-content",
                    "return_url":"https://www.pagsmile.com",
                    "notify_url":"https://www.pagsmile.com"
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",    
                    "out_uid":"out_uid",
                    "phone":"11941523675"
                    },
   ,               
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

```

>## Return

  After the request is successful, the pay link is in info. Failed info returns an error message, and the returned data is returned in json format.

  Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code |
info.trade_no | String | Yes | 128 | Pagsmile trade NO. | 2017042311015505011
info.out_trade_no | String | Yes | 128 | Merchant trade NO. | test-003192
info.total_amount | float | Yes | 10 | order amount | 10
info.currency | String | Yes | 10 | currency |
info.bank_code | String | Yes | 10 | serial number of bank side |
info.pay_url | String | Yes | 10 | pay link |

>## Success Sample

```
    {
    "code":"200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","bank_code":"88475333444003081901000004","pay_url":"https:\/\/paychanneldevin.pagsmile.com\/pagsmile\/oxxoshow?p=EC7A48BB0AB0F12653CE5514DA31525CE2C4A4EBC9DF7BEA5292D2"}
    }

```

>## Fail Sample

```
    {
    "code":"403",
    "info":"SIGN_ISNULL"
    }

```

>## Error Code

For more detailed list, please refer to[Return Status and Error List](ReturnResult)

>## Signature generation algorithm  

Reference [straight continuous signature algorithm](DriectSign)
