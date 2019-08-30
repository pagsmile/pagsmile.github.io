# Credit card payment verification interface

>## Interface link

    Test the URL address: https://paychanneldev.pagsmile.com/api/creditdo  
    Official URL address: https://paychannel.pagsmile.com/api/creditdo
    
>## Request method

     POST

>## Data Format
  
    Json
    
>## request parameters

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
App_id | String | Yes | 20 | pagsmile App ID assigned to the merchant | 2017051914172236111
Sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
Payment.out_order_no | String | Yes | 64 | Merchant Order Number |
Payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Amount range (5-14000) BRL| 88.88
Payment.currency | String | Yes | 3 | Currency | BRL
Payment.subject | String | No | 255 | Order Title |
Payment.content | String | No | 255 | Order Content |
Payment.token | String | Yes | 255 | Credit card payment credentials (valid for 7 days) |
Payment.installments | String | Yes | 12 | Credit Card Instalment | 1 No Staging Maximum 12 Staging
payment.paymentMethodId | String | Yes | 16 | Credit Card Distribution |
Payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
Customer.out_uid | String | Yes | 255 | Merchant User ID |
Customer.email | String | Yes | 255 | Email Address |
Customer.cpf_no | String | Yes | 64 | CPF Number |
Customer.username | String | Yes | 255 | User Name | User Information
Customer.buyer_ip | String | NO | 255 | Merchant user ipv4 address |
Customer.browser | String | NO | 255 | User's browser type |
Customer.phone | String | NO | 255 | Phone of the merchant's user|
Sign | String | Yes | 32 | Signature string of merchant request parameters | Signature value calculated by signature algorithm, see signature generation algorithm

 
>## Signature Description
     
     Let all the data sent or received be the set M. If there is a multi-dimensional array in the set, first obtain the one-dimensional set of the dimension, and then sort the parameters of the non-empty parameter value in the set M according to the parameter name ASCII code from small to large (dictionary) Order), use the format of the URL key-value pair (key1=value1&key2=value2...) to form a string tempData.
          - If the value of the parameter is null, it does not participate in the signature;
          - Parameter names are case sensitive;
     In the last tempData stitching, the key gets the signData string, and signData performs the MD5 operation to get the sign value signValue.
 
>## key acquisition
 
 Key setting path: merchant platform (paccess.pagsmile.com)

 For the specific setting method, please refer to [Signature Parameter Acquisition Method](/docs/signature_parameter_acquisition.pdf) 
 
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
                      'paymentMethodId' => 'visa',
                      'installments' => 3,
                      'token' => '65800b24cb695abc9e1fca12a65d7106',
                      'notify_url' => 'https://www.pagsmile.com',
                  ],
                  'customer' => [
                      'username' => 'APRO',
                      'buyer_ip' => '127.0.0.1',
                      'browser' => 'safari',
                      'email' => 'kongdexin@xcloudgame.com',
                      'cpf_no' => '50284414727',
                      'out_uid' => 'out_uid',
                      'phone' => '11941523675',
                  ],
              ]
             
 ```
 
   2. Array dimension reduction is to reduce the two-dimensional array into a one-dimensional array, before the array becomes a josn string, and the one-dimensional array is sorted by key as follows
      
```
              [
                  'app_id' => '2017051914172236111',
                  'customer' => '{"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@xcloudgame.com","cpf_no":" 50284414727","out_uid":"out_uid","phone":"11941523675"}',
                  'merchant_no' => '102320170519',
                  'payment' => '{"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject":"test-subject","content":"test-content" , "paymentMethodId":"visa","installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com"}',
                  'sign_type' => 'md5',
              ]
```
        
          
   3. According to the array, splicing according to the key value pair, and using the '&' link, get the key key in the merchant background in the last stitching of the string.
   
```
          App_id=2017051914172236111&customer={"username":"APRO","buyer_ip":"127.0.0.1","browser":"safari","email":"kongdexin@xcloudgame.com","cpf_no":"50284414727" , "out_uid": "out_uid", "phone": "11941523675"}&merchant_no=102320170519&payment={"out_order_no":"test-003630","order_amount":2000,"currency":"BRL","subject": "test-subject","content":"test-content","paymentMethodId":"visa","installments":3,"token":"65800b24cb695abc9e1fca12a65d7106","notify_url":"https://www.pagsmile.com "}&sign_type=md5&key=MD5Key
      
```
      
   4. Finally, encrypt the string with md5 to get the final sign.
    
 ```
      67073edadf3c554d0bf17555b0cd9e62
          
 ```
 
 >## Credit Card Request Sample

```
     {
             'merchant_no' => '102320170519', // ​​need to be changed to the merchant's own information according to the actual situation
             'app_id' => '2017051914172236111', // ​​need to be changed to the merchant's own information according to the actual situation
             'sign_type' => 'md5',
             'payment' => [
                 'out_order_no' => 'test-003268', //Requires to change to the merchant's own information according to the actual situation
                 'order_amount' => 2000, // ​​need to be replaced according to the actual situation of the merchant's own information
                 'currency' => 'BRL', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'subject' => 'test-subject', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'content' => 'test-content', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'paymentMethodId' => 'visa', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'installments' => 3, // ​​need to be replaced according to the actual situation of the merchant's own information
                 'token' => '65800b24cb695abc9e1fca12a65d7106', // ​​need to be replaced according to the actual situation of the merchant's own information
                 'notify_url' => 'https://www.pagsmile.com', // ​​need to be replaced according to the actual situation of the merchant's own information
             ],
             'customer' => [
                 'username' => 'APRO', // need to be replaced with the merchant's own information according to the actual situation
                 'buyer_ip' => '127.0.0.1',  / ​​need to be replaced according to the actual situation of the merchant's own information
                 'browser' => 'safari', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'email' => 'kongdexin@xcloudgame.com', // ​​need to be replaced with the merchant's own information according to the actual situation
                 'cpf_no' => '50284414727', // ​​need to be replaced according to the actual situation of the merchant's own information
                 'out_uid' => 'out_uid', // need to be replaced with the merchant's own information according to the actual situation
                 'phone' => '11941523675', // ​​need to be replaced according to the actual situation of the merchant's own information
             ],
             'sign' => '67073edadf3c554d0bf17555b0cd9e62' //Need to be changed to the merchant's own information according to the actual situation
     }
 
```
 
>## Return results

  After the request is successful. The returned data is returned in json format.

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Code | String | Yes | 16 | Return to status code |
Info.trade_no | String | Yes | 128 | Platform Order Number | 2017042311015505011
Info.out_order_no | String | Yes | 128 | Merchant Order Number | test-003192
Info.total_amount | float | Yes | 10 | Order Amount | 10
Info.currency | String | Yes | 10 | Currency |
Info.trade_status | String | Yes | 10 | Order Status | TRADE_SUCCESS

>## Successful sample

```
    {
    "code": "200",
    "info":{"trade_no":"2017111507382427391","currency":"BRL","amount":1000,"out_trade_no":"test-001","trade_status":"TRADE_SUCCESS"}
    }
```
    Trade_status has three states TRADE_SUCCESS success TRADE_REFUSED payment is rejected by the bank TRADE_RISK_CONTROL payment is reviewed within 2 hours to 2 days of review
>## Failed sample

```
    {
    "code": "403",
    "info": "SIGN_ISNULL"
    }
    
```

>## Error Code

Error Code | Description | Reason | Solution
--- | --- | --- | ---
402 | SIGN_VERIFY_FAILURE | Signature Error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
403 | SIGN_ISNULL | Unsigned | Check that the signature field in the parameter is set correctly.
405 | SIGN_TYPE_ISNULL | Signature Type Not Set | Check the parameter settings.
803 | TRADE_CURRENCY_ISNULL | Currency information not set | Check the parameter settings.
502 | MERCHANT_ID_INVALID | Merchant number not available | Check if the business number in the parameter is correct.
507 | MERCHANT_ID_NOT_ACTIVE | Merchant ID not activated | Contact customer service to see the reason for the inactivity.
602 | APP_ID_INVALID | APP number not available | Check if the APP number in the parameter is correct.
752 | CPF_NO_ISNULL | Request CPF number is empty | Check the parameter settings.
759 | EMAIL_ISNULL | Request email is empty | Check the parameter settings.
924 | CPF_INFO_NOT_MATCH | CPF information does not match |
930 | USERNAME_ISNULL | Request user name is empty | Check the parameter settings.
512 | MERCHANT_TRADE_NO_ISNULL | Merchant order number is empty | Check the parameter settings.
806 | TRADE_TIMEOUT_CLOSE | The order has expired within the specified expiration date | Check the parameter settings or confirm the order information.
400 | SYSTEM_ERROR | Order creation failed | Please try to place a new order.
550 | SINGLE_DAY_PAY_LIMIT | Exceeded single day limit | Check parameter settings or confirm order information.

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)
