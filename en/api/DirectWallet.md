# Direct Wallet API


>## API URL

    Test Environment ：https://paychanneldev.pagsmile.com/api/wallet
    Production Environment ：https://paychannel.pagsmile.com/api/wallet 
    
>## Request Method

     POST

>## Format
  
    JSON
    
>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant| 2017051914172236111
version | String | Yes | 10 | API Version, for now is fixed to: 1.0 | 1.0
timeout_express | String | Yes | 255 | Order validity | One day: 1d or 24h or 1440m;
timestamp | String | Yes | 19 | Request is sending by second | 21516081919
sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
wallet | String | Yes | 20 | Wallet type | Available types: mercadopago, picpay, ame
payment.out_order_no | String | Yes | 64 | Merchant order number |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Range (5 to 14,000) BRL | 88.88
payment.currency | String | Yes | 3 | Currency | BRL 
payment.subject | String | Yes | 255 | Order subject |
payment.content | String | Yes | 255 | Order content |
payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
payment.return_url | String | No | 255 | The http/https path of the page returned synchronously by the server. | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | Merchant's user ID |  
customer.email | String | Yes | 255 | Email address |  
customer.cpf_no | String | Yes | 64 | CPF no |  Required for mall merchants; optional for game merchants.
customer.username | String | Yes | 255 | User name | Required for mall merchants; optional for game merchants.
customer.phone | String | NO | 255 | User’s phone number|
customer.buyer_ip | String | NO | 255 | User's ipv4 address | 
customer.browser | String | NO | 255 | User's browser type|
sign | String | Yes | 32 | The signature string of the merchant request parameter | The signature value calculated by the signature algorithm. Please find details in the signature generation algorithm section.

     Note: Available wallet types are mercadopago, picpay and ame. Please use 50284414727 and Test User Name as cfp and username in the testing environment.

>## Request Sample

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "sign_type":"md5",
        "wallet":"mercadopago",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "currency":"BRL",
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
                    "cpf_no":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"11941523675"
                    },             
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## Return

  After a successful request, you may use info.qrCode to generate a QR code.

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | Return to status code | 
info.trade_no | String | Yes | 128 | Platform Order Number | 2017042311015505011
info.out_trade_no | String | Yes | 128 | Merchant Order Number| test-003192
info.total_amount | float | Yes | 10 | Order amount | 10
info.currency | String | Yes | 10 | Currency | 
info.wallet | String | Yes | 10 | Wallet type | 
info.wallet_url | String | Yes | 10 | Payment URL |

>## Success Sample

```
    { 
    "code":"200",
    "info":
            {   
                "trade_no":"2021010502431091345",
                "currency":"BRL",
                "amount":100,
                "out_trade_no":"test-003333",
                "wallet":"picpay",
                "wallet_url":"https://app.picpay.com/checkout/NWZmM2ZjNzBiMzRlYWUzZGUwM2EyNTky"
             }
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

Error Code | Description | Reason | Solution
---  | ---  | ---      | ---      
402 | SIGN_VERIFY_FAILURE | Signature error | Please follow signature rules, and verify parameter sign is set correctly
403 | SIGN_ISNULL | No signature | Please verify parameter sign is set correctly
405 | SIGN_TYPE_ISNULL | Signature type is not set | Please check parameter 
803 | TRADE_CURRENCY_ISNULL | Currency is not set | Please check parameter
502 | MERCHANT_ID_INVALID | Merchant id is not available | Please check if merchant id is correct
507 | MERCHANT_ID_NOT_ACTIVE | Merchat is not activated | Please contact customer services
602 | APP_ID_INVALID | App id is not available | Please check parameter app id
752 | CPF_NO_ISNULL | CPF is empty | Please check parameter
759 | EMAIL_ISNULL| Email is empty | Please check parameter
924 | CPF_INFO_NOT_MATCH | CPF mismatch | 
930 | USERNAME_ISNULL | Username is empty | Please check parameter
512 | MERCHANT_TRADE_NO_ISNULL | Merchant trade no is empty |Please check parameter 
806 | TRADE_TIMEOUT_CLOSE | Order expired | Please check parameter or verify your order information
400 | SYSTEM_ERROR | Failed to create the order | Please try to replace your order
550 | SINGLE_DAY_PAY_LIMIT | Over a single day limit | Please check parameter or verify your order information 

For a more details, please refer to [Return Status and Error List](https://docs.pagsmile.com/api/ReturnResult)

>## Signature generation algorithm

Please refer to [Signature generation algorithm](https://docs.pagsmile.com/api/DriectSign)

