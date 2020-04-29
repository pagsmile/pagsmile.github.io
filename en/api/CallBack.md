># Callback Notification

After the payment is completed, pagsmile will send the relevant payment result to the merchant, and the merchant needs to receive and processing，then return the response.

If pagsmile receives a response from the merchant that is not successful or the response times out, pagsmile believes that the notification failed, and will periodically re-initiate the notification through certain policies to maximize the success rate of the notification, but pagsmile does not guarantee that the notification will eventually succeed. (The notification frequency is 4/10/10/30/60/120, unit: minute)

Note: The same notification may be sent to the merchant system multiple times. The merchant system must be able to handle duplicate notifications correctly.
The recommended practice is to first check the status of the corresponding business data when it receives the notification for processing, and determine whether the notification has been processed. If it has not been processed, then processing, or if it has been processed, then the result returns successful directly. Before the status check and processing of business data, data locks should be used for concurrency control to avoid data confusion caused by function reentry.

Special reminder: The merchant system must do signature verification for the content of the payment result notification, and verify whether the returned order amount is consistent with the order amount on the merchant side, preventing data leakage from causing “false notice” and causing capital loss.

># Notification URL

The URL is set by the parameter [notify_url] submitted in the [Order API]. If the link cannot be accessed, the merchant will not be able to receive the pagsmile notification.

The notification URL must be a directly accessible url and cannot carry parameters. Example: notify_url: "https://callback.pagsmile.com/pay/callback.json"

>## Notification Parameters

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
trade_no | String | Yes | 20 | Transaction ID generated after pagsmile orders | 2018011908344902008
out_trade_no | String | Yes | 64 | Transaction ID of the corresponding merchant sent when the merchant requests the order | 
trade_status | String | Yes | 20 | Returned order status | The order status currently returned contains（TRADE_SUCCESS、TRADE_REFUND、TRADE_CHARGEBACK、TRADE_DISPUTE、PAID_MAJOR、PAID_MINOR、TRADE_REFUSED）
passback_params | String | Yes | 255 | Temporarily not be used, can be empty | 
pay_channel | String | Yes | 255 | The corresponding payment channel | 
total_amount | String | Yes | The total amount of orders | 
currency | String | Yes | 3 | currency | 
version | String Yes | 3 | Fixed to: 1.0 | 
sign_type | String | Yes | 32 | Fixed to: MD5 |  
sign | String | Yes | 32 | Reference [signature algorithm](SignatureAlgorithm)

>### Return status correspondence

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Return

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
result | String | Yes | 32 | Return result | success
