# Direct PCI Credit Card Get token

>## API URL

    Test environment: https://paychanneldev.pagsmile.com/api/getcardtoken
    Prod environment: https://paychannel.pagsmile.com/api/getcardtoken
    
>## Request format

     POST

>## Data format   
  
    json    

>## Parameter requested

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | App ID that pagsmile assigned to the merchant | 2017051914172236111
card_number | String | Yes | 20 | Credit card number | 4235647728025682
security_code | String | Yes | 4 | Security number of credit card | 123
expiration_month | String | Yes | 2 | Expiration month  | 2022
expiration_year | String | Yes | 2 | Expiration year | 12
cardholder_name | String | Yes | 100 | Credit card holder name | APRO
sign | String | Yes | 32 | Signature | 

Tip: The token is valid for 7 days, and a PCI certificate is required. No risk control measures.

>## Result

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | int | Yes | 10 | Return status code |  200success
info | string | Yes | 255 | Return info |  102.39
info.token | string | Yes | 32 | Return payment token value    | 2608f4508569a3461ddb8277844e8e62
info.card_info.first_six_digits | string | Yes | 6 | Return the first 6 digits of a credit card    | 423564
info.card_info.last_four_digits | string | Yes | 4 | Return 4 last digits of a credit card  | 5682
info.card_info.expiration_month | int | Yes | 2 | Returns credit card expiration month    | 12
info.card_info.expiration_year | int | Yes | 2 | Returns credit card expiration year    | 2022
info.card_info.cardholder_name | string | Yes | 100 | Return credit card holder name    | APRO
info.card_info.payment_method_id | string | NO | 10 | Return credit card type   | Subject to actual card

>## Return sample

```
  
  {
    "code":"200",
    "info":
        {
            "token":"2608f4508569a3461ddb8277844e8e62",
            "card_info":
                {
                    "first_six_digits":"423564",
                    "last_four_digits":"5682",
                    "expiration_month":12,
                    "expiration_year":2022,
                    "cardholder_name":"APRO"
                    "payment_method_id":"visa"
                }
        }
  }

``` 


>## Error code

Code | Description | Reason | Solution
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | Parameter type is incorrect | Check parameter settings.
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rules and confirm that the parameter sign field is set correctly.
502 | MERCHANT_ID_INVALID | Merchant number is unavailable | Check whether the merchant number is correct.
508 | MERCHANT_STATUS_ISLOCK | Merchant status is unavailable | Check if the merchant number is correct or try to contact customer service.
759 | EMAIL_ISNULL | Request email is empty | Check parameter settings.

For a more detailed list, please refer to[Return status and error list](ReturnResult)

>## Signature algorithm 

Please refer to[Signature algorithm](DriectSign)

>## After obtaining the token, please refer to the Direct PCI credit card payment verification interface


Refer to[Direct PCI credit card payment verification interface](DriectPCICreditCard)
