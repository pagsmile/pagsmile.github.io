# Credit Card Payment Page Setting


>## API URL

    Test Environment : https://paychanneldev.pagsmile.com
    Prod Environment : https://paychannel.pagsmile.com
    

>## State flow diagram

![](/assets/img/status_flow_creditcard.jpg)


>##  Form Load Content

  

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
email | String | Yes | 255 | buyer e-mail | 
cardNumber | String | Yes | 16 | buyer card number | 
securityCode | String | Yes | 4 | security code| 123
cardExpirationMonth | float | Yes | 2 |  expire year| 
cardExpirationYear | String | Yes | 4 |  expire month | 
cardholderName | String | Yes | 20 |  holder name | TEST USER NAME
installments | int | Yes | 2 |  number of installments stages | 3 reference[Instalment period chceking list](DriectCardGetinstallments)
issuer | String | Yes | 10 |  card issuing bank（auto detected by default） | 
amount | flaot | Yes | 2 |  amount of order |   

>## Form Content

Introducing security js, for security reasons, collecting card information through the merchant browser.

```
    <script src="URL/sdk/javascript/pagsmile.js"></script>
    
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
                    <label for="docType">Document type:</label>
                    <select id="docType" data-checkout="docType"></select>
                </li>
                <li>
                    <label for="docNumber">Document number:</label>
                    <input type="text" id="docNumber" data-checkout="docNumber" name="cpf_no" placeholder="12345678" />
                </li>
                <li>
                    <select id="issuer" style="display:none">
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


Introduce js code to get transaction parameters

```
       Pagsmile.setPublishableKey(merchant_no,app_id); //Get page encryption public key
    
       Pagsmile.getIdentificationTypes(); //Check required fields
        
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
        
        // Get the credit card payment method, judge the issuing bank through the first 6 digits of the card
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
            
        // Get the installment amount
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
        
        // Verify payment security information
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
    
        // Payment to get token verification code
        function doPay(event){
            event.preventDefault();
            if(!doSubmit){
                var $form = document.querySelector('#pay');
    
                Pagsmile.createToken($form, sdkResponseHandler); // The function "sdkResponseHandler" is defined below
    
                return false;
            }
        };
        
        // Set the number of installments and amount
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
        
        // Create hidden fields to collect information and submit it to the merchant server
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

Test Data:  

Type | Card NO. | Organization | CVC |Expire Date | Holder Name | CPF | CEP
--- | --- | --- | --- | --- | --- | ---| ---
Credit Card | 4235647728025682 | VISA | 123 | 12/2020 | APRO | 50284414727 | 38082365
Credit Card | 5031433215406351 | MasterCard | 123 | 12/2020 | APRO | 50284414727 | 38082365

Please refer to the [credit card payment verification interface](DriectCreditdo) after the page is submitted. addEvent(document.querySelector('#pay'), 'submit', doPay);
