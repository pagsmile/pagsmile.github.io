#Instalment period chceking list(by amount)

>## Interface link

    Test Environment : https://paychanneldev.pagsmile.com/api/getinstallments  
    Prod Environment: https://paychannel.pagsmile.com/api/getinstallments
    
>## Request method

     POST

>## Data Format
  
    Json

>## request parameters

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
App_id | String | Yes | 20 | pagsmile App ID assigned to the merchant | 2017051914172236111
Amount | String | Yes | 20 | Instalment query order amount (there will be a period limit according to the amount of the amount, the larger the amount, the more the number of periods is up to 12) | 100
Sign | String | Yes | 32 | Signature |

Tip: When you send a refund request, the order must be in a successful state.

>## Return results

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Installments | int | Yes | 10 | Number of returns | 2
Installment_amount | float | Yes | 10 | Return Period Amount | 102.39
Total_amount | float | Yes | 10 | Total deduction amount | 204.78


>## Return results

```
 {
 
 "1":{"installments":1,"installment_amount":200,"total_amount":200},
 
 "2":{"installments":2,"installment_amount":102.39,"total_amount":204.78},
 
 "3":{"installments":3,"installment_amount":69.85,"total_amount":209.56},
 
 "4":{"installments":4,"installment_amount":53.59,"total_amount":214.34},
 
 "5":{"installments":5,"installment_amount":43.6,"total_amount":217.98},
 
 "6":{"installments":6,"installment_amount":36.83,"total_amount":220.98},
 
 "7":{"installments":7,"installment_amount":31.95,"total_amount":223.66},
 
 "8":{"installments":8,"installment_amount":28.12,"total_amount":224.98},
 
 "9":{"installments":9,"installment_amount":25.16,"total_amount":226.42},
 
 "10":{"installments":10,"installment_amount":22.92,"total_amount":229.18},
 
 "11":{"installments":11,"installment_amount":21.09,"total_amount":232},
 
 "12":{"installments":12,"installment_amount":19.57,"total_amount":234.82}
 
 }

``` 


>##  Error Code

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature generation algorithm

Reference straight [continuous signature algorithm](SignatureAlgorithm)
