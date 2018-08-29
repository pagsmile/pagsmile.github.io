# 签名算法

>## 签名说明
    
    设所有发送或者接收到的数据为集合M，如果集合内有多维数组则先进行将维得到一维集合后，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（key1=value1&key2=value2…）拼接成字符串tempData。
         - 如果参数的值为空不参与签名；
         - 参数名区分大小写；
    在tempData最后拼接上key得到signData字符串，并signData进行MD5运算，得到sign值signValue。

>## key的获取

key设置路径：商户平台(paccess.pagsmile.com)
    
具体设置方式请参照 [签名参数获取方法](/docs/接口参数获取方法.docx)  

>## 样例
    
1. 将一个多位数组进行降维。降维前数组如下
    
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
2. 数组降维就是将二维数组都降成一维数组，之前是数组的变成一个josn串，并将该一维数组按照key排序如下

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

3. 按照数组按照键值对拼接，并使用'&'链接，在字符串最后拼接上在商户后台得到对密钥key
 
    ```
        app_id=2017051914172236111&customer={"name":"Test User Name","buyer_ip":"127.0.0.1","browser":"safari","email":"test@pagsmile.com","cpf":"50284414727","out_uid":"out_uid","phone":"11941523675"}&merchant_no=102320170519&payment={"out_order_no":"test-003803","order_amount":10,"currency":"BRL","subject":"test-subject","content":"test-content","method":"103001","return_url":"www.pagsmile.com","notify_url":"www.pagsmile.com"}&sign_type=md5&timeout_express=15d&timestamp=1516190481&version=1.0&key=MD5Key
    
    ```
    
4. 最后将字符串用md5加密得到最后的sign
  
    ```
    9c359d0c63f468186ae7ea529cf202b3    
    ```

