# Direct credit card payment PCI verification interface


>## API URL

    Test environment：https://paydev.luxpag.com/api/creditpci
    Prod environment：https://pay.luxpag.com/api/creditpci 
    
>## Request method

     POST

>## Data format   
  
    JSON
    
>## Request parameter

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID assigned to the merchant by Pagsmile | 1024201708140012289
app_id | String | Yes | 20 | App ID assigned to the merchant by Pagsmile | 2017051914172236111
sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
payment.out_order_no | String | Yes | 64 | Merchant order number |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Amount range (5-14000) BRL| 88.88
payment.currency | String | Yes | 3 | Currency | BRL 
payment.subject | String | Yes | 255 | Order title |
payment.content | String | Yes | 255 | Order content |
payment.token | String | Yes | 255 | Credit card payment voucher (valid for 7 days) |
payment.installments | String | Yes | 12 | Credit card installments | 1 no installments, up to 12
payment.payment_method_id | String | Yes | 16 | Credit card issuing organization |
payment.notify_url | String | Yes | 255 | Http/https path of specific page in the server of merchant to which our server will actively send notifications | https://www.test.com
customer.out_uid | String | Yes | 255 | User ID in merchant's system |  
customer.email | String | Yes | 255 | Email of the user |  
customer.identification | String | Yes(NO) | 64 | User information mark | Required when currency is BRL
customer.identification.type | String | Yes | 50 | Document type of the user |  CPF
customer.identification.number | String | Yes | 50 | Document ID |  50284414727
customer.username | String | Yes | 255 | User name | Maria João de Silva
customer.zip_code | String | Yes | 10 | User zip code | 58000-000 
customer.country | String | NO | 10 | User country | Brazil 
customer.city | String | NO | 10 | User city | São Paulo 
customer.bill_address | String | NO | 255 | User billing address | User billing address
customer.buyer_ip | String | NO | 255 | User ipv4 address | 
customer.browser | String | NO | 255 | The user's browser type|
customer.phone | String | NO | 255 | Phone number of the user|
sign | String | Yes | 32 | Signature string of merchant request parameters | The signature value calculated by the signature algorithm, see the signature algorithm for details

 Note: identification is required when currency is BRL.
 
 >## Signature algorithm
     
     Suppose that all the data sent or received is set M. If there is a multi-dimensional array in the set, first get a one-dimensional set from the dimensions, and sort the parameters of non-empty parameter values in set M according to the ASCII code of the parameter name from small to large (Dictionary Sequence), using the URL key-value pair format (key1=value1&key2=value2...) to be spliced into a string tempData.
           -If the parameter value is empty, it will not participate in the signature;
           -The parameter name is case sensitive;
      At the end of tempData, the key is spliced to get the signData string, and signData performs MD5 operation to get the sign value signValue.
 
 >## Get key
 
 Where to configure key：merchant dashboard (paccess.pagsmile.com)
     
 For more details please refer to [Signature parameter acquisition method](/docs/接口参数获取方法.pdf)  
 
 >## Signature sample
     
 1. Reduce the dimensionality of a multi-digit array. The array before dimensionality reduction is as follows
     
     ```
      [
          'merchant_no' => '102320170519',
          'app_id' => '2017051914172236111',
          'sign_type' => 'md5',
          'payment' => [
              'out_order_no' => 'test-003630',
              'order_amount' => 2000,
              'currency' => 'BRL',
              'subject' => 'test-subject',
              'content' => 'test-content',
              'payment_method_id' => 'visa',
              'installments' => 3,
              'token' => '65800b24cb695abc9e1fca12a65d7106',
              'notify_url' => 'https://www.test.com',
          ],
          'customer' => [
              'username' => 'APRO',
              'buyer_ip' => '127.0.0.1',
              'browser' => 'safari',
              'email' => 'kongdexin@test.com',
              'cpf_no' => '50284414727',
              'out_uid' => 'out_uid',
              'phone' => '11941523675',
              'identification' => [
                          'type' => 'CPF',
                          'number' => '50284414727',
                      ],
          ],
      ]
     
     ```
 2. Array dimensionality reduction is to reduce all two-dimensional arrays to one-dimensional arrays. The previous array becomes a JSON string, and the one-dimensional array is sorted by key as follows
 
     ```
         [
             'app_id' => '2017051914172236111',
             'customer' => '{"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@test.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}',
             'merchant_no' => '102320170519',
             'payment' => '{"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.test.com"}',
             'sign_type' => 'md5',
         ]
         
     ```
 
 3. According to the array according to the key-value pair splicing, and use the'&' link, the last splicing of the string to get the key pair in the merchant backstage
  
     ```
         app_id=2017051914172236111&customer={"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@test.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}&merchant_no=102320170519&payment={"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.test.com"}&sign_type=md5&key=MD5Key
     
     ```
     
 4. Finally, encrypt the string with md5 to get the final sign
   
     ```
     67073edadf3c554d0bf17555b0cd9e62
         
     ```

>## Request sample of credit card

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003169",
                    "order_amount":1000,
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",
                    "paymentMethodId":"visa",
                    "installments":3,
                    "token":"ce0559644ebe1251fa036ff95ea790d6",
                    "notify_url":"https:\/\/www.test.com"
                   },
        "customer":{
                      "username":"APRO",
                      "buyer_ip":"127.0.0.1",
                      "browser":"safari",
                      "email":"kongdexin@test.com",
                      "out_uid":"out_uid",
                      "phone":"11941523675",
                      "zip_code":"38082365",   
                      "bill_address":"city test",
                      "identification":{
                                    "type":"CPF",
                                    "number":"50284414727"
                                       }
                       }    
    }
    
 ``` 

>## Return result

  After the request is successful. The returned data is returned in json format.

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | Return status code | 
info.trade_no | String | Yes | 128 | Order ID in Pagsmile | 2017042311015505011
info.out_order_no | String | Yes | 128 | Order ID of the merchant system| test-003192
info.total_amount | float | Yes | 10 | Order amount | 10
info.currency | String | Yes | 10 | Currency | 
info.trade_status | String | Yes | 10 | Order status | TRADE_SUCCESS

>## Success sample

```
    {
    "code":"200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","trade_status":"TRADE_SUCCESS"}
    }
    
```
    "trade_status" has 3 status: TRADE_SUCCESS (Success)  TRADE_REFUSED (Order is refused by bank) TRADE_RISK_CONTROL （The payment is under review, and the review result will be received within 2 hours to 2 days）
    
>## Failure sample

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```

>## Error code

Code | description | Reason | Solution
---  | ---  | ---  | ---
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rules and confirm that the parameter sign field is set correctly.
403 | SIGN_ISNULL | Not signed | Check whether the signature field in the parameter is set correctly.
405 | SIGN_TYPE_ISNULL | The signature type is not set | Check the parameter settings.
803 | TRADE_CURRENCY_ISNULL | Currency information is not set | Check parameter settings.
502 | MERCHANT_ID_INVALID | Merchant ID is not available | Check whether the merchant ID in the parameter is correct.
507 | MERCHANT_ID_NOT_ACTIVE | Merchant ID is not activated | Contact customer service to check the reason for not activation.
602 | APP_ID_INVALID | APP number is not available | Check whether the APP number in the parameter is correct.
752 | CPF_NO_ISNULL | Request CPF number is empty | Check parameter settings.
759 | EMAIL_ISNULL | Request email is empty | Check parameter settings.
924 | CPF_INFO_NOT_MATCH | CPF information does not match |
930 | USERNAME_ISNULL | The requested user name is empty | Check the parameter settings.
512 | MERCHANT_TRADE_NO_ISNULL | Merchant order number is empty | Check parameter settings.
806 | TRADE_TIMEOUT_CLOSE | The order has exceeded the specified expiration time | Check the parameter settings or confirm the order information.
400 | SYSTEM_ERROR | Order creation failed | Please try to place another order.
550 | SINGLE_DAY_PAY_LIMIT | Single day limit exceeded | Check parameter settings or confirm order information.

For more details please refer to [Return status and error list](ReturnResult)
