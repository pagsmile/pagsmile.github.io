---
title: Signature Algorithm
category: enapi
order: 2
language: en
---

# Signature algorithm

### 1. How To Signature
  
Let all the data sent or received be the set M. If there is a multi-dimensional array in the set, first obtain the one-dimensional set of the dimension, and then sort the parameters of the non-empty parameter value in the set M according to the parameter name ASCII code from small to large (dictionary) Order), use the format of the URL key-value pair (key1=value1&key2=value2...) to form a string tempData.
  - If the value of the parameter is null, it does not participate in the signature;
  - Parameter names are case sensitive;

In the last tempData stitching, the key gets the signData string, and signData performs the MD5 operation to get the sign value signValue.

### 2. How To Get the Key?

  Where? : [Merchant platform](https://paccess.pagsmile.com)
    
  For more details, please refer to [signature parameter acquisition](/docs/signature_parameter_acquisition.pdf);  

### 3. Sample
    
1. Dimension a multi-bit array. The array before dimension reduction is as follows
    
    ```
     [
        'merchant_no' => '102320170519',
        'app_id' => '2017051914172236111',
        'timestamp' => 1516190481,
        'version' => '1.0',
        'timeout_express' => '15d',
        'sign_type' => 'md5',
        'payment' => [
            'out_order_no' => 'test-003803',
            'order_amount' => 10,
            'currency' => 'BRL',
            'subject' => 'test-subject',
            'content' => 'test-content',
            'method' => '103001',
            'return_url' => 'www.pagsmile.com',
            'notify_url' => 'www.pagsmile.com',
        ],
        'customer' => [
            'name' => 'Test User Name',
            'buyer_ip' => '127.0.0.1',
            'browser' => 'safari',
            'email' => 'test@pagsmile.com',
            'cpf' => '50284414727',
            'out_uid' => 'out_uid',
            'phone' => '11941523675',
        ],
    ]
    
    ```
2. Array dimension reduction is to reduce the two-dimensional array into a one-dimensional array, before the array becomes a josn string, and the one-dimensional array is sorted by key as follows

    ```
        [
            'app_id' => '2017051914172236111',
            'customer' => '{"name":"Test User Name","buyer_ip":"127.0.0.1","browser":"safari","email":"test@pagsmile.com","cpf":"50284414727","out_uid":"out_uid","phone":"11941523675"}',
            'merchant_no' => '102320170519',
            'payment' => '{"out_order_no":"test-003803","order_amount":10,"currency":"BRL","subject":"test-subject","content":"test-content","method":"103001","return_url":"www.pagsmile.com","notify_url":"www.pagsmile.com"}',
            'sign_type' => 'md5',
            'timeout_express' => '15d',
            'timestamp' => 1516190481,
            'version' => '1.0',
        ]
    ```

3. According to the array, splicing according to the key value pair, and using the '&' link, get the key key in the merchant background in the last stitching of the string
 
    ```
        app_id=2017051914172236111&customer={"name":"Test User Name","buyer_ip":"127.0.0.1","browser":"safari","email":"test@pagsmile.com","cpf":"50284414727","out_uid":"out_uid","phone":"11941523675"}&merchant_no=102320170519&payment={"out_order_no":"test-003803","order_amount":10,"currency":"BRL","subject":"test-subject","content":"test-content","method":"103001","return_url":"www.pagsmile.com","notify_url":"www.pagsmile.com"}&sign_type=md5&timeout_express=15d&timestamp=1516190481&version=1.0&key=MD5Key
    
    ```
    
4. Finally, the string is encrypted with md5 to get the final sign
  
    ```
    9c359d0c63f468186ae7ea529cf202b3    
    ```
