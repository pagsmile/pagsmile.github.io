---
title: DriectCrebitCancel
category: enapi
order: 17
language: en
---
# CreditCard Cancel API

### 1. API URL

    test URL: https://paychanneldev.pagsmile.com/api/cancel
    prod URL: https://paychannel.pagsmile.com/api/cancel
    
### 2. Request Method

     POST

### 3. Format 
  
    json    

### 4. Request Parameters

Parameter | Type | Required | Maximum length | Description | Example
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
App_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
Trade_no | String | Yes | 255 | Pagsmile order number for refund | 2018022604263906847
Sign | String | Yes | 32 | Signature |

Note: When you send a refund request, the order must be in a successful status.

### 5. Return

Parameter | Type | Required | Maximum length | Description | Example
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code | success:200
info | String | Yes | 128 | information | 
data | String | Yes | 256 | null    |

### 6. Error Code

For a more detailed list, please refer to [Return Status and Error List](../ReturnResult)

### 7. Signature Generation Algorithm

Reference [Signature Algorithm](../SignatureAlgorithm)
