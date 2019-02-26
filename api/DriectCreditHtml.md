# 商户信用卡下单页面设置


>## 

>## 接口链接

    测试URL地址：https://paychanneldev.pagsmile.com
    正式URL地址：https://paychannel.pagsmile.com
    
    
    
>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
merchant_no | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
app_id | String | Yes | 20 | pagsmile分配给商户的应用ID | 2017051914172236111
sign_type | String | Yes | 10 | 目前仅支持MD5 | MD5
payment.out_order_no | String | Yes | 64 | 商户订单号 |
payment.order_amount | String | Yes | 10 | 订单总金额，精确到小数点后两位。金额范围（5-14000） BRL| 88.88
payment.currency | String | Yes | 3 | 币种 | BRL 
payment.subject | String | No | 255 | 订单标题 |
payment.content | String | No | 255 | 订单内容 |
payment.token | String | No | 255 | 信用卡支付凭据（有效期7天） |
payment.paymentMethodId | String | No | 10 | 发卡行 |visa
payment.installments | int | No | 4 | 信用卡分期期数 | 3
payment.notify_url | String | Yes | 255 | 服务器主动通知商户服务器里指定的页面http/https路径。 | https://www.pagsmile.com
customer.out_uid | String | No | 255 | 商户的用户ID |  
customer.email | String | Yes | 255 | 邮箱地址 |  
customer.cpf_no | String | Yes | 64 | CPF号码 | 
customer.username | String | Yes | 255 | 用户姓名 | 用户信息
customer.buyer_ip | String | NO | 255 | 商户的用户ipv4地址 | 
customer.browser | String | NO | 255 | 商户的用户浏览器类型|
customer.phone | String | NO | 255 | 商户的用户的电话|
sign | String | Yes | 32 | 商户请求参数的签名串 | 通过签名算法计算得出的签名值，详见签名生成算法




>## 返回结果

   表单加载内容

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
email | String | Yes | 16 | 用户邮箱 | 
cardNumber | String | Yes | 16 |用户卡号 | 
securityCode | String | Yes | 4 | 安全码| 123
cardExpirationMonth | float | Yes | 2 |  信用卡过期时间月份| 
cardExpirationYear | String | Yes | 4 |  信用卡过期时间年份 | 
cardholderName | String | Yes | 20 |  持卡人姓名 | TEST USER NAME
installments | int | Yes | 2 |  信用卡分期期数 | 3
issuer | String | Yes | 10 |  发卡行（默认自动获取） | 
amount | flaot | Yes | 2 |  分期金额 |   

>## 表单内容

引入安全js，处于安全考虑,通过商户浏览器收集卡信息。

```
    <script src="URL地址/sdk/javascript/pagsmile.js"></script>
    
```

```
    <form action="credit" method="post" id="pay" name="pay" >
        <fieldset>
            <ul>
                <li>
                  
                    <label for="email">Email</label>
                    <input id="email" name="email" value="test_user_19653727@testuser.com" type="email" placeholder="your email"/>
                </li>
                <li>
                    <label for="cardNumber">Credit card number:</label>
                    <input type="text" id="cardNumber" data-checkout="cardNumber" placeholder="4509 9535 6623 3704" onselectstart="return false" onpaste="return false" onCopy="return false" onCut="return false" onDrag="return false" onDrop="return false" autocomplete=off />
                </li>
                <li>
                    <label for="securityCode">Security code:</label>
                    <input type="text" id="securityCode" data-checkout="securityCode" placeholder="123" onselectstart="return false" onpaste="return false" onCopy="return false" onCut="return false" onDrag="return false" onDrop="return false" autocomplete=off />
                </li>
                <li>
                    <label for="cardExpirationMonth">Expiration month:</label>
                    <input type="text" id="cardExpirationMonth" data-checkout="cardExpirationMonth" placeholder="12" onselectstart="return false" onpaste="return false" onCopy="return false" onCut="return false" onDrag="return false" onDrop="return false" autocomplete=off />
                </li>
                <li>
                    <label for="cardExpirationYear">Expiration year:</label>
                    <input type="text" id="cardExpirationYear" data-checkout="cardExpirationYear" placeholder="2015" onselectstart="return false" onpaste="return false" onCopy="return false" onCut="return false" onDrag="return false" onDrop="return false" autocomplete=off />
                </li>
                <li>
                    <label for="cardholderName">Card holder name:</label>
                    <input type="text" id="cardholderName" name="cardholderName" data-checkout="cardholderName" placeholder="APRO" />
                </li>
                <li>
                    <label for="installments">installments:</label>
                    <select id="installments" data-checkout="installments" name="installments" placeholder="installments" ></select>
                </li>
                <li>
                    <label for="docType">Document type:</label>
                    <select id="docType" data-checkout="docType"></select>
                </li>
                <li>
                    <label for="docNumber">Document number:</label>
                    <input type="text" id="docNumber" data-checkout="docNumber" name="cpf_no" placeholder="12345678" />
                </li>
                <li>
                    <select id="issuer" >
                        <option value="issuer"  >Issuer</option>
                    </select>
                </li>
            </ul>
                <input type="hidden" id="amount" value="100"  />
            </ul>
    
            <input type="hidden" name="paymentMethodId" />
            <input type="submit" value="Pay!" />
        </fieldset>
    </form>
    
```


引入js代码获取交易参数

```
        //merchant_no pagsmile分配给商户的ID
        //app_id  pagsmile分配给商户的应用ID
    
       Pagsmile.setPublishableKey(merchant_no,app_id); //获取页面加密公钥
    
       Pagsmile.getIdentificationTypes(); //检查必填字段
        
        function addEvent(el, eventName, handler) {
    
            if (el.addEventListener) {
    
    
                try{
    
                    el.addEventListener(eventName, handler);
    
                    // el.addEventListener(eventName, handler);
                }catch (e){
    
                    console.log(e);
    
                }
            } else {
                el.attachEvent('on' + eventName, function () {
                    handler.call(el);
                });
            }
        }
        
        //获取信用卡支付方式，通过卡的前6位判断发卡行
        function guessingPaymentMethod(event) {
            var bin = getBin();
    
            if (event.type == "keyup") {
                if (bin.length >= 6) {
                    Pagsmile.getPaymentMethod({
                        "bin": bin
                    }, setPaymentMethodInfo);
                }
            } else {
                setTimeout(function() {
                    if (bin.length >= 6) {
                        Pagsmile.getPaymentMethod({
                            "bin": bin
                        }, setPaymentMethodInfo);
                    }
                }, 100);
            }
        };
        
        
        function cardsHandler() {
            clearOptions();
            var cardSelector = document.querySelector("#cardId"),
                amount = document.querySelector('#amount').value;
            if (cardSelector && cardSelector[cardSelector.options.selectedIndex].value != "-1") {
                var _bin = cardSelector[cardSelector.options.selectedIndex].getAttribute("first_six_digits");
                Pagsmile.getPaymentMethod({
                    "bin": _bin
                }, setPaymentMethodInfo);
            }
        }
            
        //获取分期金额    
        function setInstallmentInfo(status, response) {
            var selectorInstallments = document.querySelector("#installments"),
                fragment = document.createDocumentFragment();
    
            selectorInstallments.options.length = 0;
    
            if (response.length > 0) {
                var option = new Option("Choose...", '-1'),
                    payerCosts = response[0].payer_costs;
    
                fragment.appendChild(option);
                for (var i = 0; i < payerCosts.length; i++) {
                    option = new Option(payerCosts[i].recommended_message || payerCosts[i].installments, payerCosts[i].installments);
                    fragment.appendChild(option);
                }
                selectorInstallments.appendChild(fragment);
                selectorInstallments.removeAttribute('disabled');
            }
        }
        
        //验证支付安全信息
        function setPaymentMethodInfo(status, response) {
            if (status == 200) {
                var form = document.querySelector('#pay');
                var paymentMethod = document.createElement('input');
                paymentMethod.setAttribute('name', "paymentMethodId");
                paymentMethod.setAttribute('type', "hidden");
                paymentMethod.setAttribute('value', response[0].id);
    
                form.appendChild(paymentMethod);
    
                
                var cardConfiguration = response[0].settings,
                    bin = getBin(),
                    amount = document.querySelector('#amount').value;
    
                Pagsmile.getInstallments({
                    "bin": bin,
                    "amount": amount
                }, setInstallmentInfo);
    
               
                var issuerMandatory = false,
                    additionalInfo = response[0].additional_info_needed;
    
                for (var i = 0; i < additionalInfo.length; i++) {
                    if (additionalInfo[i] == "issuer_id") {
                        issuerMandatory = true;
                    }
                }
                if (issuerMandatory) {
                    Pagsmile.getIssuers(response[0].id, showCardIssuers);
                    addEvent(document.querySelector('#issuer'), 'change', setInstallmentsByIssuerId);
                } else {
                    document.querySelector("#issuer").style.display = 'none';
                    document.querySelector("#issuer").options.length = 0;
                }
    
            } else {
                document.querySelector("input[name=paymentMethodId]").value = response[0].id;
            }
        }
    
        //支付获取token验证码
        function doPay(event){
            event.preventDefault();
            if(!doSubmit){
                var $form = document.querySelector('#pay');
    
                Pagsmile.createToken($form, sdkResponseHandler); // The function "sdkResponseHandler" is defined below
    
                return false;
            }
        };
        
        //设置分期期数和金额
        function setInstallmentsByIssuerId(status, response) {
            var issuerId = document.querySelector('#issuer').value,
                amount = document.querySelector('#amount').value;

    
            if (issuerId === '-1') {
                return;
            }
    
            Pagsmile.getInstallments({
                "bin": getBin(),
                "amount": amount,
                "issuer_id": issuerId
            }, setInstallmentInfo);
        }
        
        //创建隐藏字段讲收集信息，提交到商户服务器
        function sdkResponseHandler(status, response) {
            if (status != 200 && status != 201) {
                alert("verify filled data");
            }else{
                var form = document.querySelector('#pay');
                var card = document.createElement('input');
                card.setAttribute('name', 'token');
                card.setAttribute('type', 'hidden');
                card.setAttribute('value', response.id);
                form.appendChild(card);
                doSubmit=true;
                form.submit();
            }
        };
        
        //获取卡bin号
        function getBin() {
            var cardSelector = document.querySelector("#cardId");
            var de = JSON.stringify(cardSelector);
            if (cardSelector && cardSelector[cardSelector.options.selectedIndex].value != "-1") {
                return cardSelector[cardSelector.options.selectedIndex].getAttribute('first_six_digits');
            }
    
            var ccNumber = document.querySelector('input[data-checkout="cardNumber"]');
            return ccNumber.value.replace(/[ .-]/g, '').slice(0, 6);
        }
        
        
        function clearOptions() {
            var bin = getBin();
            if (bin.length == 0) {
    
                document.querySelector("#issuer").style.display = 'none';
                document.querySelector("#issuer").innerHTML = "";
    
                var selectorInstallments = document.querySelector("#installments"),
                    fragment = document.createDocumentFragment(),
                    option = new Option("Choose...", '-1');
    
                selectorInstallments.options.length = 0;
                fragment.appendChild(option);
                selectorInstallments.appendChild(fragment);
                selectorInstallments.setAttribute('disabled', 'disabled');
            }
        }
    
        doSubmit = false;
        addEvent(document.querySelector('input[data-checkout="cardNumber"]'), 'keyup', guessingPaymentMethod);
        addEvent(document.querySelector('input[data-checkout="cardNumber"]'), 'keyup', clearOptions);
        addEvent(document.querySelector('input[data-checkout="cardNumber"]'), 'change', guessingPaymentMethod);
        cardsHandler();
        addEvent(document.querySelector('#pay'), 'submit', doPay);
    
```
测试数据:  

类型 | 卡号 | 卡组织 | cvc | 有效期 | 持卡人姓名 | CPF号码 | CEP
--- | --- | --- | --- | --- | --- | ---
信用卡 | 4235647728025682 | visa | 123 | 12/2020 | APRO | 50284414727
信用卡 | 5031433215406351 | mastercard | 123 | 12/2020 | APRO | 50284414727


>## 页面提交后请参考信用卡支付验证接口

参考直[信用卡支付验证接口](DriectCreditdo)

