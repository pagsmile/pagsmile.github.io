# Boleto Order API


>## API URL

    test URL：https://paychanneldev.pagsmile.com/api/boleto
    prod URL：https://paychannel.pagsmile.com/api/boleto 
    
>## Request Method

     POST

>## Format
  
    json
    
>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | Pagsmile ID assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Apps ID assigned to the merchant by pagsmile | 2017051914172236111
version | String | Yes | 10 | Fixed to: 1.0 | 1.0
timeout_express | String | Yes | 255 | Order validity | The time of day is assigned: 1d or 24h or 1440m;
timestamp | String | Yes | 19 | The time unit for sending the request is seconds | 21516081919
sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
payment.out_order_no | String | Yes | 64 | Merchant order number |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. | 88.88
payment.currency | String | Yes | 3 | currency | BRL 
payment.subject | String | No | 255 | subject |
payment.content | String | No | 255 | content |
payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
payment.return_url | String | No | 255 | The page http/https path returned by the server synchronization. | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | Merchant's user ID |  
customer.email | String | Yes | 255 | email address |  
customer.cpf_no | String | Yes | 64 | CPF | Mall merchants are required here; game merchants are optional.
customer.username | String | Yes | 255 | user name | Mall merchants are required here; game merchants are optional.
customer.buyer_ip | String | NO | 255 | user's ipv4 address | 
customer.browser | String | NO | 255 | user's browser type|
customer.phone | String | NO | 255 | user's phone No.|
address.zip_code | String | Yes | 8-8 | zip_code| 06233-200
address.street_name | String | Yes | 70 | street_name| Av. das Nações Unidas
address.street_number | String | Yes | 10 | street_number| 3003
address.neighborhood | String | Yes | 50 | neighborhood| Bonfim
address.city | String | Yes | 50 | city| Osasco
address.federal_unit | String | Yes | 2-2 | federal_unit| SP
sign | String | Yes | 32 | The signature string of the merchant request parameter | The signature value calculated by the signature algorithm is detailed in the signature generation algorithm.

     Note: The boleto currency currently only supports USD and BRL. The cpf and username used in the test environment are 50284414727 and Test User Name.

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

  After the request is successful, the boleto download link is in info. Failed info returns an error message, and the returned data is returned in json format.

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | 
info | String | Yes | 128 | information | 

>## Success Sample

```
    { 
    "code":"200",
    "info":"https:\/\/meiosdepagamentobradesco.com.br\/apiboleto\/Bradesco?token=aTExSlFpbm51MW9XbFFXa2xyaERCTkUrNjArZ2dISUQyYktnSGVtTzJLNWlBSlVSMkQvNnp2MDc4aEJzMFR2aw.."
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

>## Signature generation algorithm

Reference straight [continuous signature algorithm](SignatureAlgorithm)

