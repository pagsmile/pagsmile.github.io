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
Merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
App_id | String | Yes | 20 | pagsmile application ID assigned to the merchant | 2017051914172236111
Trade_no | String | Yes | 255 | Pagsmile order number for refund | 2018022604263906847
Email | String | Yes | 255 |
Refund_amount | Float | Yes | 255 | Request a refund amount
Currency | String | Yes | 255 | Request a refund currency
Description | String | No | 255 | Refund description
Sign | String | Yes | 32 | Signature |

Tip: When you send a refund request, the order must be in a successful state.

>## Return

Parameter | Type | Required | Maximum length | Description | Example
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | 200:成功
info | String | Yes | 128 | information | SUCCESS
data | String | Yes | 256 | null    |

>## Error Code

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature Generation Algorithm

Reference [Direct Connection Signature Algorithm](DriectSign)RefundApply.md
