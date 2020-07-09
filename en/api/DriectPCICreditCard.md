# Direct credit card payment PCI verification interface


>## API URL

    Test environment：https://paychanneldev.pagsmile.com/api/creditpci
    Prod environment：https://paychannel.pagsmile.com/api/creditpci 
    
>## Request method

     POST

>## Data format   
  
    JSON
    
>## Request parameter

Parameter | Type | Required | Max length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID assigned to the merchant by Pagsmile | 1024201708140012289
app_id | String | Yes | 20 | App ID assigned to the merchant by Pagsmile | 2017051914172236111
sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
payment.out_order_no | String | Yes | 64 | Merchant order number |
payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. Amount range (5-14000) BRL| 88.88
payment.currency | String | Yes | 3 | Currency | BRL 
payment.subject | String | Yes | 255 | Order title |
payment.content | String | Yes | 255 | Order content |
payment.token | String | Yes | 255 | Credit card payment voucher (valid for 7 days) |
payment.installments | String | Yes | 12 | Credit card installments | 1 no installments, up to 12
payment.payment_method_id | String | Yes | 16 | Credit card issuing organization |
payment.notify_url | String | Yes | 255 | Http/https path of specific page in the server of merchant to which our server will actively send notifications | https://www.pagsmile.com
customer.out_uid | String | Yes | 255 | Merchant's user ID |  
customer.email | String | Yes | 255 | Email address of user |  
customer.identification | String | Yes(NO) | 64 | User information label | Required when currency is 
