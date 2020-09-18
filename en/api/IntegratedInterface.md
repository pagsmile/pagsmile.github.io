# Integrated Interface

>## Flow

![](/assets/img/CreateOrderFlow01.png)

>## URL

    Test : https://testenv.pagsmile.com/pserver/gateway.json  
    Prod : https://pserver.pagsmile.com/gateway.json

>## Request Parameters

NAME | TYPE | REQUIRED | MAX LENGTH | DESCRIPTION | EXAMPLE
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | ID that pagsmile assigned to the merchant | 1024201708140012289
app_id | String | Yes | 20 | Application ID that pagsmile assigned to the merchant | 2017051914172236111
method | String | No | 11 | Payment channel ID | 101(Credit Card) ; 103(Boleto) ; 106(Deposite Express) ; 107(Pagamento na loterica) ; 108(OXXO) ; 109(Citibanamex) ; 111(BBVA Bancomer) ; 112(Santander)|
out_order_no | String | Yes | 64 | Merchant order number |
out_uid | String | Yes | 64 | Merchant's user ID |
subject | String | Yes | 255 | Order Subject |
content | String | Yes | 255 | Order content |
order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. | 88.88
currency | String | Yes | 3 | Currency | BRL、PHP、MXN、RUB
email | String | No | 255 | Email |  
cpf_no | String | No | 64 | CPF number | Mall merchants are required here; game merchants are optional.
username | String | No | 255 | User Name | Mall merchants are required here; game merchants are optional.
charset | String | Yes | 10 | The encoding format requested | utf-8
timestamp | String | Yes | 19 | The time the request was sent, the format "yyyy-MM-dd HH:mm:ss" | 2018-01-08 15:27:26
version | String | Yes | 10 | API Version, for now is fixed to 1.0 | 1.0
timeout_express | String | Yes | 255 | Order validity | 1d；1h；1m
passback_params | String | Yes | 255 | Request return parameters |
notify_url | String | No | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com/openapi/notify.json
return_url | String | No | 255 | The http/https path of the page returned synchronously by the server. | https://www.pagsmile.com/success.html
billing_cycle | String | No | 4 | 订阅付费的计费周期（日；月；年） | 1D；1M；1Y
trial_price | String | No | 10 | 订阅付费首单优惠价格，精确到小数点后两位 | 99.99
trial_period | String | No | 4 | 订阅付费首单优惠的持续时间（日；月；年） | 1D；1M；1Y
sign_type | String | Yes | 10 | Only MD5 is supported | MD5
sign | String | Yes | 32 | The signature string of the merchant request parameter | The signature value calculated by the signature algorithm is detailed in the signature generation algorithm.

Note: Method  Payment channal ID

124(Recurrings) ; 101(Credit Card) ; 103(Boleto) ; 106(Deposite Express) ; 107(Pagamento na loterica) ; 108(OXXO) ; 109(Citibanamex) ; 111(BBVA Bancomer) ; 112(Santander) ; 115(GCash) ; 118(wallet)

Recurring payment is a payment initiated by a merchant. Such payments are deducted monthly. After the client's first payment is successful, the next month's payment time is the same as the previous month's payment time, and the merchant can deduct the money without additional client consent. Recurring payment will stop the deduction after the deduction fails or the merchant cancels it.

Pagsmile will notify the cardholder by email of the creation of each payment, any successful/failed payments and the status of the payments.

Test Data :  

Card Type | Card No. | Organization | CPF | Name | CVS | Validity
--------- | -------- | ------------ | --- | ---- | --- | --------
Credit card | 4235647728025682 | visa | 50284414727 | APRO | 123 | 12/2020
Credit card | 5031433215406351 | mastercard | 50284414727 | APRO | 123 | 12/2020
Credit card(MXN) | 4075595716483764 | visa |  | APRO | 123 | 12/2020
Credit card(MXN) | 5474925432670366 | mastercard |  | APRO | 123 | 12/2020
Deposit Express | / | / | 50284414727 | Test User Name | / | /

Reference arrival time:  

region | method | amount limit | settled time
Brazil | Credit Card/Card virtual | 0.5~50000 (BRL) | Instant, or 1~4 day(s) when risk-controlled  
Brazil | Boleto： | 5~ (BRL) | In 5m~3d after paid  
Brazil | Deposit Express | 4~50000 (BRL) | In 4 hour after paid  
Brazil | Lottery： | 4~2000 (BRL) | In 1 hour after paid  
Mexico | Credit Card | 5~200000 (MXN) | Instant, or 1~4 day(s) when risk-controlled  
Mexico | OXXO | 5~10000 (MXN) | In 1~2 day(s) after paid  
Mexico | Citibanamex/Santander/BBVA Bancomer | 10~40000 (MXN) | In 1 day after paid  
Philippines | GCash | 1~10000 (PHP) | Instant  

>## Response Parameters

NAME | TYPE | REQUIRED | MAX LENGTH | DESC | EXAMPLE
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | response status code |
info | String | Yes | 128 | response message |

>## Error Code List

CODE | DESC | REASON | SOLUTION
---  | ---  | ---  | ---
551 | IP_REQUEST_TOO_FAST_LIMIT | Single IP request is too frequent | Check for malicious bills
402 | SIGN_VERIFY_FAILURE | Signature error | Set the signature according to the given rule and confirm that the parameter sign field is set correctly.
403 | SIGN_ISNULL | Unsigned | Check that the signature field in the parameter is set correctly.
405 | SIGN_TYPE_ISNULL | Signature type not set | Check the parameter settings.
803 | TRADE_CURRENCY_ISNULL | Currency information is not set | Check the parameter settings.
502 | MERCHANT_ID_INVALID | Merchant number is not available | Check if the business number in the parameter is correct.
507 | MERCHANT_ID_NOT_ACTIVE | Merchant number is not activated | Contact customer service to see the reason for the inactivity.
602 | APP_ID_INVALID | APPID is not available | Check if the APP number in the parameter is correct.
752 | CPF_NO_ISNULL | CPF number is empty | Check the parameter settings.
924 | CPF_INFO_NOT_MATCH | CPF information does not match |
512 | MERCHANT_TRADE_NO_ISNULL | Merchant order number is empty | Check the parameter settings.
806 | TRADE_TIMEOUT_CLOSE | The order has exceeded the specified expiration time | Check the parameter settings or confirm the order information.
400 | SYSTEM_ERROR | Order creation failed | Please try to place a new order.
550 | SINGLE_DAY_PAY_LIMIT | More than one day limit | Check the parameter settings or confirm the order information.


>## Signature generation algorithm  

1. Let all the data sent or received be the set M, and sort the parameters of the non-empty parameter values in the set M according to the parameter name ASCII code from small to large (dictionary order), using the format of the URL key-value pair (key1=value1&key2= Value2...) is stitched into a string tempData.
     - If the value of the parameter is null, do not participate in the signature,
     - Parameter names are case sensitive.

2. In the last tempData stitching on the key to get the signData string, and signData to perform MD5 operation, get the sign value signValue
    - Key setting path: merchant platform(https://paccess.pagsmile.com)

>## demo

SEE : [PHP Demo](DemoPHP)
