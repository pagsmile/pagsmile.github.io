# Order inquiry interface

>## API URL

    test URL: https://paychanneldev.pagsmile.com/api/checkorder
    prod URL: https://paychannel.pagsmile.com/api/checkorder
    
>## Request method

     POST

>## Format
  
    json    

>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
trade_no/out_trade_no | String | Yes | 255 | Pagsmile order number that requesting a refund or merchant custom order number | 2018022604263906847
sign | String | Yes | 32 | Signature | 


>## Returns

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | success:200 
info | String | Yes | 128 | information | success: SUCCESSFUL
data.merchant_no | String | Yes | 50 | ID that pagsmile assigned to the merchant  
data.app_id | String | Yes | 50 | Application ID that pagsmile assigned to the merchant
data.callback_status | String | Yes | 50 | Whether the order callback is successful 
data.order_currency | String | Yes | 50 | currency  
data.out_uid | String | Yes | 50 | User identifier such as user id
data.order_amount | String | Yes | 50 | Order amount
data.trade_status | String | Yes | 50 | Order status
data.trade_no | String | Yes | 50 |  Pagsmile transaction serial number

>## Error Code

code | Description | Reason | Solution
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | The package type is incorrect | Check the parameter settings.
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
502 | MERCHANT_ID_INVALID | Merchant number is not available | Check whether the merchant number in the parameter is correct.
508 | MERCHANT_STATUS_ISLOCK | Merchant status is not available | Check whether the merchant number in the parameter is correct or try to contact customer service.
759 | EMAIL_ISNULL | Request email is empty | Check the parameter settings.

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature generation algorithm

Reference [signature algorithm](SignatureAlgorithm)
