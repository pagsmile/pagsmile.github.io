# CreditCard Installment API

>## API URL

    test URL：https://paychanneldev.pagsmile.com/api/recurrent
    prod URL：https://paychannel.pagsmile.com/api/recurrent 
    
>## Request Method

     POST

>## Format 
  
    json
    
>## Request Parameters

Parameter | Type | Required | Maximum length | Description | Example
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
App_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
Version | String | Yes | 10 | The version of the interface being called, fixed at: 1.0 | 1.0
Timeout_express | String | Yes | 255 | Order Validity | One-day assignment: 1d or 24h or 1440m;
Passback_params | String | Yes | 255 | Transparent pass parameters | default passback_params
Timestamp | String | Yes | 19 | Request is sending by second | 21516081919
Sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
Payment.out_order_no | String | Yes | 64 | Merchant Order Number |
Payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. | 88.88
Payment.currency | String | Yes | 3 | Currency | BRL
Payment.method | String | Yes | 10 | Channel Code (default) | 101001001
Payment.installments | int | Yes | 2 | Staging Period | 2 to 12
Payment.subject | String | No | 255 | Order Subject |
Payment.content | String | No | 255 | Order Content |
Payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
Payment.return_url | String | No | 255 | The http/https path of the page returned synchronously by the server. | https://www.pagsmile.com
Payment.authenticate | int | No | 4 | Do cardholder authorization is needed(default) | 0 or 1
Payment.authenticate_back_url | String | No | 255 | Jump link after authorization. (must be required when payment.authenticate is 1) | https://www.pagsmile.com
Payment.credit_card.number | String | Yse | 19 | Card Number | 455187******0183
Payment.credit_card.holder | String | Yse | 255 | Cardholder Name. | Test User Name
payment.credit_card.expirationDate | String | Yse | 7 | Credit card overdue time. | 12/2030
payment.credit_card.securityCode | String | Yse | 4 | Credit card security code. | 123
Payment.credit_card.brand | String | No | 10 | Credit card issuer. (visa,master,amex,elo,aura,jcb,dinners,discover) | visa
Customer.out_uid | String | No | 255 | Merchant User ID |
Customer.email | String | No | 255 | Email Address |
Customer.cpf_no | String | Yes | 64 | CPF Number | Mall Merchants are required here; Game Merchants are optional.
Customer.username | String | Yes | 255 | User Name | Mall Merchants are required here; Game Merchants are optional.
Customer.buyer_ip | String | No | 255 | User’s ipv4 address |
Customer.browser | String | No | 255 | User's browser type |
Customer.phone | String | No | 255 | User’s Phone number|
Address.zip_code | String | No | 8-8 | User's mailing address zip code | 06233-200
Address.street_name | String | No | 70 | User's mailing address Street name | Av. das Nações Unidas
Address.street_number | String | No | 10 | User's mailing address Street number | 3003
Address.neighborhood | String | No | 50 | User's mailing address community address | Bonfim
Address.city | String | No | 50 | User's mailing address for the city | Osasco
Address.federal_unit | String | No | 2 | State abbreviation for user's mailing address | SP
Sign | String | Yes | 32 | Signature string of merchant request parameters | Signature value calculated by signature algorithm, see signature generation algorithm

     Note: The currency currently only supports USD and BRL, the cpf_no. and username which is used in the test environment    
           is 50284414727 and Test User Name.
     
     Test card number, card type is not limited, recommend visa
        
        Success 0000000000000001 or 0000000000000004
        Fail    0000000000000002 or 0000000000000008
     

>## Request Sample

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "passback_params":"passback_params",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "method":"101001001",
                    "installments":"4"
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",
                    "return_url":"www.pagsmile.com",
                    "notify_url":"www.pagsmile.com",
                    "authenticate":0,
                    "authenticate_back_url":"www.pagsmile.com",
                    "credit_card":{
                        "number":"0000000000000001",
                        "holder":"Test User Name",
                        "expirationDate":"12/2020",
                        "securityCode":"123",
                        "brand":"visa"
                    }
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
        "address":{
                    "zip_code":"06233-200",
                    "street_name":"Av. das Nações Unidas",
                    "street_number":"3003",
                    "neighborhood":"Bonfim",
                    "city":"Osasco",
                    "federal_unit":"SP"
                    },               
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## Return

After the request is successful, the returned data is in info. The returned data is returned in json format.

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Code | String | Yes | 16 | Return to status code (success is 200) | 200
Info.trade_status | String | Yes | 128 | Return to order status | TRADE_SUCCESS
Info.trade_no | String | Yes | 128 | Platform Order Number | 2017042311015505011
Info.out_order_no | String | Yes | 128 | Merchant Order Number | test-003192
Info.total_amount | float | Yes | 10 | Order Amount | 10
Info.currency | String | Yes | 10 | Currency |

>## Success Sample

```
    { 
    "code":"200",
    "info":{"trade_status":"TRADE_SUCCESS","trade_no":"2018042311015505011","out_order_no":"test-003192","total_amount":10,"currency":"BRL"}
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

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature Generation Algorithm

Reference [Signature Algorithm](SignatureAlgorithm)

>## Enable authorization link

Refer to [Enable Authorization Link](AuthenticateUrl)
