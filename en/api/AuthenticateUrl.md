# Enable authorization link

>## Authorized link description
    
   The user needs to go to the issuing bank to log in and authorize before performing the authorization operation.
         

>## After opening the authorization

    After the authorization is successful, an authorization jump link will be returned.

>## Parameters
    
Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | status code (success is 200)| 200
info | String | Yes | 128 | Returned authentication link | https:\/\/authorizationmocksandbox.cieloecommerce.cielo.com.br\/CardAuthenticator\/Receive\/7984d820-a136-400f-98a4-1db86b9104f5

   Description: After the test environment authorization link jump is obtained, the jump operation is performed. In the select selection box, the authorization of 'Autenticado' is successful, and the authorization of 'Não autenticado' fails.
 

Successfully obtained an example of an authorized link

```
    { 
    "code":"200",
    "info":"https:\/\/authorizationmocksandbox.cieloecommerce.cielo.com.br\/CardAuthenticator\/Receive\/7984d820-a136-400f-98a4-1db86b9104f5"
    }
    
```

1. After the authorization is successful, the authorization link provided to the merchant will send an array of authorization success in POST mode.

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
status | String | Yes | 16 | return status| 200 | success
trade_no | String | Yes | 128 | pagsmile trading order number |  2018042311570804284
info | String | Yes | 128 | information |  success


    
    ```
        {
              ["status"]=>
              string(7) "success"
              ["trade_no"]=>
              string(19) "2018042311570804284"
              ["info"]=>
              string(8) "success "
        }
        
    ```


2. After the authorization fails, the authorization link provided to the merchant will send an array of authorization failures in POST mode.

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
status | String | Yes | 16 | status| failed | failed
trade_no | String | Yes | 128 | pagsmile trading order number |  2018042311570804284
info | String | Yes | 128 | information |  bank-91-failed



    ```
        {
               ["status"]=>
               string(7) "failed"
               ["trade_no"]=>
               string(19) "2018042311570804284"
               ["info"]=>
               string(8) "bank-91-failed "
        }
    ```
    
   

