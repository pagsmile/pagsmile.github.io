# Payout Apply Interface Description

>## Interface link

    Test the URL address: https://paychanneldev.pagsmile.com/api/payoutapply  
    Official URL address: https://paychannel.pagsmile.com/api/payoutapply
    
>## Request method

     POST

>## Data Format
  
    Json

>## request parameters

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
App_id | String | Yes | 20 | pagsmile App ID assigned to the merchant | 2017051914172236111
Email | String | Yes | 255 | Email requesting a transfer
Name | String | Yes | 255 | Transferee Name
Phone | String | Yes | 11 | Transfer Phone
Cpf_no | String | Yes | 11 | Transferr cpf
Amount | Float | Yes | 255 | Request a transfer amount
Currency | String | Yes | 3 | Request Amount Currency | BRL
Bank_id | String | Yes | 10 | Transferr Bank Number (Refer to [Brazil Bank Payment List](Bankinfo))
Agency | String | Yes | 6 | Transferor branch code
Account_no | Int | Yes | 20 | Transferring bank account number
Account_type | String | Yes | 1 | Transferring bank account type 0 savings_account 1 checking_account
Notify_url | String | 255 | 20 | Transfer result notification address | https://www.pagsmile.com
Sign | String | Yes | 32 | Signature |



>## Return results

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Code | String | Yes | 16 | Return to status code | 200: Request successful
Info.trade_no | String | Yes | 128 | Successfully returned transfer number | 2019080904564629463
Data | String | Yes | 256 | Current state description | SYSTEM_PARAM_ERROR

>## Error Code

Error Code | Description | Reason | Solution
--- | --- | --- | ---
401 | SYSTEM_PARAM_ERROR | Package type is incorrect | Check the parameter settings.
402 | SIGN_VERIFY_FAILURE | Signature Error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
502 | MERCHANT_ID_INVALID | Merchant number not available | Check if the business number in the parameter is correct.
508 | MERCHANT_STATUS_ISLOCK | Merchant status not available | Check if the business number in the parameter is correct or try to contact customer service.
759 | EMAIL_ISNULL | Request email is empty | Check the parameter settings.

For a more detailed list, please refer to [Return Status and Error List] (ReturnResult)

>## Signature Generation Algorithm

Reference [Signature Algorithm] (DriectSign)