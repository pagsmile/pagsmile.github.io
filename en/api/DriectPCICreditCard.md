# Direct credit card payment PCI verification interface


>## API URL

    Test environment：https://paychanneldev.pagsmile.com/api/creditpci
    Prod environment：https://paychannel.pagsmile.com/api/creditdopci 
    
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
payment.notify_url | String | Yes | 255 | Http/https path of specific page in the server of merchant to which our server will actively send notifications | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | Merchant's user ID |  
customer.email | String | Yes | 255 | Email address of user |  
customer.identification | String | Yes(NO) | 64 | User information label | Required when currency is BRL
customer.identification.type | String | Yes | 50 | User Information Type |  CPF
customer.identification.number | String | Yes | 50 | User information id |  50284414727
customer.username | String | Yes | 255 | User name | User info
customer.buyer_ip | String | NO | 255 | User's ipv4 address | 
customer.browser | String | NO | 255 | Type of user's browser |
customer.phone | String | NO | 255 | Phone number of user |
sign | String | Yes | 32 | Signature string of the merchant request | The signature value calculated by the signature algorithm, see the signature description for details

Tip: identification is required when the currency is BRL
 
 >## Signature instructions
     
     Let all the data sent or received be the set M. If there is a multi-dimensional array in the set, first obtain the one-dimensional set of the dimension, and then sort the parameters of the non-empty parameter value in the set M according to the parameter name ASCII code from small to large (dictionary) Order), use the format of the URL key-value pair (key1=value1&key2=value2…) to form a string tempData.
          - If the value of the parameter is null, it does not participate in the signature;
          - Parameter names are case sensitive;
     In the last tempData stitching, the key gets the signData string, and signData performs the MD5 operation to get the sign value signValue.
 
 >## How to get the key?
 
 Where：merchant dashboard(paccess.pagsmile.com)
     
 For more details, please refer to [signature parameter acquisition](/docs/signature parameter acquisition.pdf)  
 
 >## Signature sample
     
 1. Dimension a multi-bit array. The array before dimension reduction is as follows
     
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
              'notify_url' => 'https://www.pagsmile.com',
          ],
          'customer' => [
              'username' => 'APRO',
              'buyer_ip' => '127.0.0.1',
              'browser' => 'safari',
              'email' => 'kongdexin@pagsmile.com',
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
 2. Array dimension reduction is to reduce the two-dimensional array into a one-dimensional array, before the array becomes a josn string, and the one-dimensional array is sorted by key as follows
 
     ```
         [
             'app_id' => '2017051914172236111',
             'customer' => '{"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@pagsmile.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}',
             'merchant_no' => '102320170519',
             'payment' => '{"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com"}',
             'sign_type' => 'md5',
         ]
         
     ```
 
 3. According to the array, splicing according to the key value pair, and using the ‘&’ link, get the key key in the merchant background in the last stitching of the string
     ```
         app_id=2017051914172236111&customer={"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@pagsmile.com","out_uid":"out_uid","phone":"11941523675","identification":{"type":"CPF","number":"50284414727"}}&merchant_no=102320170519&payment={"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content","payment_method_id":'visa',"installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com"}&sign_type=md5&key=MD5Key
     
     ```
     
 4. Finally, the string is encrypted with md5 to get the final sign
   
     ```
     67073edadf3c554d0bf17555b0cd9e62
         
     ```

>## Sample of credit card request

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
                    "payment_method_id":"visa",
                    "installments":3,
                    "token":"ce0559644ebe1251fa036ff95ea790d6",
                    "notify_url":"https:\/\/www.pagsmile.com"
                   },
        "customer":{
                      "username":"APRO",
                      "buyer_ip":"127.0.0.1",
                      "browser":"safari",
                      "email":"kongdexin@pagsmile.com",
                      "out_uid":"out_uid",
                      "phone":"11941523675",
                      "identification":{
                                    "type":"CPF",
                                    "number":"50284414727"
                                       }
                       }    
    }
    
 ``` 

>## Results

  After the request is successful. The returned data is returned in json format.

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | Return status code | 
info.trade_no | String | Yes | 128 | Platform order number | 2017042311015505011
info.out_order_no | String | Yes | 128 | Merchant order number | test-003192
info.total_amount | float | Yes | 10 | Oder amount | 10
info.currency | String | Yes | 10 | Currency | 
info.trade_status | String | Yes | 10 | Order status | TRADE_SUCCESS

>## Success sample

```
    {
    "code":"200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","trade_status":"TRADE_SUCCESS"}
    }
    
```
    There are 3 statuses of trade_status TRADE_SUCCESS success  TRADE_REFUSED the payment is refused by bank TRADE_RISK_CONTROL payment under review takes 2 hours to 2 days
    
>## Failure example

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```

>## Error code

Code | Description | Reason | Solution
---  | ---  | ---  | ---
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rules and confirm that the parameter sign field is set correctly.
403 | SIGN_ISNULL | Unsigned | Check that the signature fields in the parameters are set correctly.
405 | SIGN_TYPE_ISNULL | Signature type is not set | Check parameter settings.
803 | TRADE_CURRENCY_ISNULL | Currency information is not set | Check parameter settings.
502 | MERCHANT_ID_INVALID | Merchant number is not available | Check whether the merchant number in the parameters is correct.
507 | MERCHANT_ID_NOT_ACTIVE | Merchant number is not activated | Contact customer service for the reason for the inactivation.
602 | APP_ID_INVALID | APP number is not available | Check whether the APP number in the parameters is correct.
752 | CPF_NO_ISNULL | Request CPF number is empty | Check parameter settings.
759 | EMAIL_ISNULL | Request email is empty | Check parameter settings.
924 | CPF_INFO_NOT_MATCH | CPF does not match | 
930 | USERNAME_ISNULL | Request user name is empty | Check parameter settings.
512 | MERCHANT_TRADE_NO_ISNULL | Merchant order number is empty | Check parameter settings.
806 | TRADE_TIMEOUT_CLOSE | The order has exceeded the specified expiry date | Check parameter settings or confirm order information.
400 | SYSTEM_ERROR | Order creation failed | Please try to place your order again.
550 | SINGLE_DAY_PAY_LIMIT | Exceeded one-day limit | Check parameter settings or confirm order information.

For more details please refer to [Return status and error list](ReturnResult)



