# 支付接口php demo

>## 集成接口下单demo

```
     <?php
    
    	$appkey = 'MD5Key';//商户后台app创建key
    
        $order_time = date('Y-m-d H:i:s',time()); //下单时间
    
        $order_data = array(
                'merchant_no' => '102320170519', //商户编号
                'app_id' => '2017051914172236111', //商户后台创建的app编号
                'method' => '',//空为集成页面 101003002(Credit Card); 102001(Debit Card) ; 103001(Boleto) ; 110010(Deposite Express)
                'out_order_no' =>'merchant_order_001',//商户订单号
                'out_uid' => 'merchant_uid_001', //商户用户唯一标示
                'cpf_no' => '50284414727',  //巴西用户身份编号
                'username' =>'Test User Name', //用户姓名
                'email'=> 'test@pagsmile.com', //用户邮箱
                'subject' => 'order subject',  //订单标题
                'content' => 'order content',  //订单内容
                'order_amount' => '13.14',    //金额
                'currency' => 'BRL', //币种
                'charset' => 'utf-8', //编码默认
                'timestamp' => $order_time, //下单时间
                'version' => '1.0', //默认
                'timeout_express' => '15d', //订单过期时间
                'passback_params' => 'passback_params', //透出参数，回调原样返回
                'sign_type' => 'md5',//加密方式
                'notify_url' => 'www.pagsmile.com', //异步通知
                'return_url' => 'www.pagsmile.com' //同步跳转
            );
    
        ksort($order_data);
    
        $str = '';
    
        foreach ($order_data as $key => $value) {
    
                if (!empty($order_data[$key])) {
    
                    $str = $str . '&' . $key . '=' . $value;
                }
    
        }
       
    
        $str .= "&key=" . $appkey;
        
        $str = substr($str, 1);
    
        echo $str;
    
        $sign = md5($str);

     ?>
    
    <html>
    <head><title> pagesmile</title></head>
    <body>
    <form id="pagsmile_pay" method="post" name="pagsmile_pay" action="https://testenv.pagsmile.com:8443/pserver/gateway.json">
    
        <!-- Pagsmile Configuration -->
        <input type="hidden" name="merchant_no" value="<?php echo $order_data['merchant_no']?>">
        <input type="hidden" name="app_id" value="<?php echo $order_data['app_id']?>">
        <input type="hidden" name="method" value="<?php echo $order_data['method']?>">
        <input type="hidden" name="out_order_no" value="<?php echo $order_data['out_order_no']?>">
        <input type="hidden" name="cpf_no" value="<?php echo $order_data['cpf_no']?>">
        <input type="hidden" name="username" value="<?php echo $order_data['username']?>">
        <input type="hidden" name="out_uid" value="<?php echo $order_data['out_uid']?>">
        <input type="hidden" name="subject" value="<?php echo $order_data['subject']?>">
        <input type="hidden" name="content" value="<?php echo $order_data['content']?>">
        <input type="hidden" name="order_amount" value="<?php echo $order_data['order_amount']?>">
        <input type="hidden" name="currency" value="<?php echo $order_data['currency']?>">
        <input type="hidden" name="charset" value="<?php echo $order_data['charset']?>">
        <input type="hidden" name="timestamp" value="<?php echo $order_data['timestamp']?>">
        <input type="hidden" name="version" value="<?php echo $order_data['version']?>">
        <input type="hidden" name="email" value="<?php echo $order_data['email']?>">
        <input type="hidden" name="timeout_express" value="<?php echo $order_data['timeout_express']?>">
        <input type="hidden" name="passback_params" value="<?php echo $order_data['passback_params']?>">
        <input type="hidden" name="notify_url" value="<?php echo $order_data['notify_url']?>">
        <input type="hidden" name="return_url" value="<?php echo $order_data['return_url']?>">
        <input type="hidden" name="sign_type" value="<?php echo $order_data['sign_type']?>">
        <input type="hidden" name="sign" value="<?php echo  $sign?>">
    
        <center><font face="Verdana, Arial, Helvetica, sans-serif" size="2" color="333333">Go to payment ...</font></center>
    
    </form>
    
    <script>document.getElementById("pagsmile_pay").submit();</script>
    </body>
    </html>

```

 

>## 支付异步回调验证签名demo
    
```
      <?php
    
            echo 'success'; //成功收到回调的通知
    
            $appkey = 'MD5Key'; //商户后台app创建key
    
            $response = $_POST;
    
            //sign不参与签名删除
            $sign = $response['sign'];
    
            unset($response['sign']);
      
            ksort($response);
    
            $str = '';
    
            foreach ($response as $key => $value) {
    
                if (!empty($response[$key])) {
    
                    $str = $str . '&' . $key . '=' . $value;
                }
    
            }
            $str .= "&key=" . $appkey;
        
            $str = substr($str, 1);
    
            $sign_v = md5($str);
        
            if($sign == $sign_v){
    
            	//successful code
    
            }
    
    ?>
    
```