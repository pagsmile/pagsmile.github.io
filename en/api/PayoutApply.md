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
merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile App ID assigned to the merchant | 2017051914172236111
email | String | Yes | 255 | Email requesting a transfer | test@pagsmile.com
name | String | Yes | 255 | Transferee Name | Test User Name
phone | String | Yes | 11 | Transfer Phone  | 13512345678
cpf_no | String | Yes | 11 | Transferr cpf  | 50284414727
amount | Float | Yes | 255 | Request a transfer amount | 100.1
currency | String | Yes | 3 | Request Amount Currency | BRL
bank_id | String | Yes | 10 | Transferr Bank Number (Refer to [Brazil Bank Payment List](Bankinfo)) | 318
agency | String | Yes | 6 | Transferor branch code | 123456
account_no | String | Yes | 15 | Transferring bank account number | 123456789012-34
account_type | String | Yes | 1 | Transferring bank account type 1 savings_account 2 checking_account | 1
notify_url | String | 255 | 20 | Transfer result notification address | https://www.pagsmile.com | https://www.pagsmile.com
sign | String | Yes | 32 | Signature |



>## Return results

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
code | String | Yes | 16 | Return to status code | 200: Request successful
info.trade_no | String | Yes | 128 | Successfully returned transfer number | 2019080904564629463
data | String | Yes | 256 | Current state description | SYSTEM_PARAM_ERROR

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
