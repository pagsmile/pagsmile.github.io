# php demo

>## demo

```
     <?php
    
    	$appkey = 'MD5Key';
    
        $order_time = date('Y-m-d H:i:s',time()); 
    
        $order_data = array(
                'merchant_no' => '102320170519', 
                'app_id' => '2017051914172236111', 
                'method' => '',
                'out_order_no' =>'merchant_order_001'.time(),
                'out_uid' => 'merchant_uid_001',
                'cpf_no' => '50284414727', 
                'username' =>'Test User Name', 
                'email'=> 'test@pagsmile.com', 
                'subject' => 'order subject',  
                'content' => 'order content',  
                'order_amount' => '13.14', 
                'currency' => 'BRL', 
                'charset' => 'utf-8', 
                'timestamp' => $order_time, 
                'version' => '1.0', 
                'timeout_express' => '15d',
                'passback_params' => 'passback_params',
                'sign_type' => 'md5',
                'notify_url' => 'www.pagsmile.com',
                'return_url' => 'www.pagsmile.com'
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
    
        $sign = md5($str);

     ?>
    
    <html>
    <head><title> pagesmile</title></head>
    <body>
    <form id="pagsmile_pay" method="post" name="pagsmile_pay" action="http://testenv.pagsmile.com/pserver/gateway.json">
    
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

 

>## sign demo
    
```
      <?php
    
            echo 'success';
    
            $appkey = 'MD5Key';
    
            $response = $_POST;
    
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
