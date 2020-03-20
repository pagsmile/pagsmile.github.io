# Refund API

>## API URL

    test URL: https://paychanneldev.pagsmile.com/api/refundapply
    prod URL: https://paychannel.pagsmile.com/api/refundapply

>## Request Method

     POST

>## Format   

    json    

>## Request Parameters

Parameter | Type | Required | Maximum length | Description | Example
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
trade_no | String | Yes | 255 | Pagsmile order number for refund | 2018022604263906847
out_request_no | String | Yes | 255 | The merchant's serial number requesting a refund (there will be an asynchronous notification after successful) |  2018022604263906847
email | String | Yes | 255 | Refund email
refund_amount | Float | Yes | 255 | Refund amount
description | String | No | 255 | description
bank_info | String | No | 3 | yes when bank_info is with request parameters, empty as default
name | String | No（bank_info=yes Yes） | 255 | name
cpf_no | String | No（bank_info=yes Yes） | 11 | CPF
bank_id | String | No（bank_info=yes Yes） | 10 | bank_id（reference to[Bank List in Brasil](Bankinfo)）
bank_name | String | No（bank_info=yes Yes） | 50 | bank_name（reference to[Bank List in Brasil](Bankinfo)）
agency | String | No（bank_info=yes Yes） | 6 | branch code
account_no | Int | No（bank_info=yes Yes） | 20 | acount
account_type | Int | No（bank_info=yes Yes） | 1 | acount type 1 savings_account 2 checking_account
sign | String | Yes | 32 | sign |

Note: When you send a refund request, the order must be in a successful status.
The bank_info information is not required. It is convenient for the user to receive the refund after the user has provided the personal transfer account information. The default is empty and can be used when collecting user banking information.

>## Return

Parameter | Type | Required | Maximum length | Description | Example
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | 200:success
info | String | Yes | 128 | information | SUCCESS
data | String | Yes | 256 | null    |

>## Error Code

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature Generation Algorithm

Reference [Direct Connection Signature Algorithm](SignatureAlgorithm)
