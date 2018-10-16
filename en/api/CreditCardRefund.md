# Credit Card Refund API


>## API URL

    test URL：https://paychanneldev.pagsmile.com/api/refund
    prod URL：https://paychannel.pagsmile.com/api/refund 
    
>## Request Method

     POST

>## Format
  
    json
    
>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | Pagsmile ID assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Apps ID assigned to the merchant by pagsmile | 2017051914172236111
method   | String | Yes | 10 | Channel code (default 101001) | 101001 
trade_no | String | Yes | 19 | pagsmile trading order number | 2018042311015505011
sign | String | Yes | 32 | signature | The signature value calculated by the signature algorithm is detailed in the signature generation algorithm.

    

>## Returns

  After the request is successful, the returned data is in info. The returned data is returned in json format.

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code| 200
info | String | Yes | 128 | information | REFUND_SUCCESSFUL

>## Success Sample

```
    { 
    "code":"200",
    "info": "REFUND SUCCESSFUL"
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

code | Description | Reason | Solution
---  | ---  | ---  | ---
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
403 | SIGN_ISNULL | Unsigned | Check that the signature field in the parameter is set correctly.



>## Signature generation algorithm

Reference [signature algorithm](DriectSign)

>## Enable authorization link

Refer to [Enable Authorization Link](AuthenticateUrl)
