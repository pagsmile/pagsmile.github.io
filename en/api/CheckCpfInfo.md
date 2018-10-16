# CPF Verification

>## API URL

    test URL: https://paychanneldev.pagsmile.com/api/checkcpf
    prod URL: https://paychannel.pagsmile.com/api/checkcpf
    
>## Request method

     POST

>## Format
  
    json    

>## Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | Pagsmile ID assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Apps ID assigned to the merchant by pagsmile | 2017051914172236111
type | String | Yes | 2 | Request packet type: 1 for basic verification, CPF number and name verification; 2 for advanced verification, verification includes name, gender, mother's name, birthday information. | 1或2
cpf_no | String | Yes | 11 | CPF number Requested verification without special symbol | 
username | String | Yes | 255 | User's name Requested for verification
nameOfMom | String | Yes(type=2) | 255 | Mother's name Requested verification (required only in advanced verification)
birthday | String | Yes(type=2) | 10 | Birthday Requested verification (required only in advanced verification) | DD/MM/YYYY
gender | String | Yes(type=2) | 1 | Gender requested for verification (required only in advanced verification) | （M \| F）
sign | String | Yes | 32 | signature | 

Test: use cpf in the test environment and the name corresponds to 50284414727 and Test User Name

>## Returns

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | 200:success
info | String | Yes | 128 | information | 
data | String | Yes | 256 | data | Query remaining number of times

>## Error Code

code | Description | Reason | Solution
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | Package type is incorrect | Check the parameter settings.
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
502 | MERCHANT_ID_INVALID | Merchant number is not available | Check if the business number in the parameter is correct.
508 | MERCHANT_STATUS_ISLOCK | Merchant status is not available | Check if the merchant number in the parameter is correct or try to contact customer service.
509 | MERCHANT_REQUEST_REFUSED | Merchant request rejected | If the number of merchant interface requests is insufficient or there is no request permission, please contact customer service to open.
752 | CPF_NO_ISNULL | Request CPF number is empty | Check the parameter settings.
924 | CPF_INFO_NOT_MATCH | CPF information does not match | 

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature generation algorithm

Reference [signature algorithm](DriectSign)
