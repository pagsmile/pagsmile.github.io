# Cancellation API of Recurring Payments

>## URL

    Test: https://paychanneldev.pagsmile.com/api/cancelsubscription
    Prod: https://paychannel.pagsmile.com/api/cancelsubscription
    
>## Request Method

     POST

>## Data Format   
  
    Json    

>## Request Parameters

Parameter | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
trade_no | String | Yes | 255 | Pagsmile order ID of the transaction that needs to be cancelled | 2018022604263906847
sign | String | Yes | 32 | Signature | 

Note：Only one day after the payment is made successfully, you can cancel the recurring payment.

>## Return Parameters 

Parameter | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | Return status code | Success:200 
info | String | Yes | 128 | Return info | Success: success
 
>## Error Code

Code | Description | Reason | Solution
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | The parameter is incorrect | Check the parameter settings. 
402 | SIGN_VERIFY_FAILURE | Sign error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
502 | MERCHANT_ID_INVALID | The merchant ID is unavailable | Check the merchant ID.
508 | MERCHANT_STATUS_ISLOCK | The merchant status is lock | Check if the merchant ID is correct or contact Pagsmile.
759 | EMAIL_ISNULL | The email field is blank | Check the parameter settings.

For more details please refer to [Return Status and Error List](ReturnResult)

>## Signature generation algorithm 

Please refer to [Signature generation algorithm](DriectSign)
