># Recurring Payment Callback Notification

After the recurring payment is turned on, pagsmile will send the relevant payment results and user information to the merchant, who needs to receive and process, and return a response("success").

When interacting with notifications, if pagsmile receives a response from the merchant that is not "success" or timed out, Pagsmile considers that the notification has failed, and will periodically re-initiate notifications through certain strategies to increase the success rate of the notification as much as possible, but Pagsmile does not guarantee that the notification will eventually succeed . (The notification frequency is 4/10/10/30/60/120, unit: minute)

Note: The same notification may be sent to the merchant system multiple times. The merchant system must be able to properly handle duplicate notifications.
The recommended approach is to first check the status of the corresponding business data when receiving a notification for processing, to determine whether the notification has been processed, if it has not been processed, then process it, and if it is processed, return the result directly. Before the status check and processing of business data, data locks should be used for concurrency control to avoid data confusion caused by function reentry.

Special reminder: The merchant system must perform signature verification for the content of the payment result notification, and verify whether the returned order amount is consistent with the order amount on the merchant side to prevent data leakage from causing "false notifications" and causing financial losses.

># Callback address

The address is set by the parameter notify_url submitted in the [create order API]. If the address is not accessible, the merchant will not receive Pagsmile notifications.

The callback address must be a directly accessible URL and cannot have parameters. Example：notify_url：“https://callback.pagsmile.com/pay/callback.json”

>## Callback Parameter

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
subscription_no | String | Yes | 20 | Subscription ID of Pagsmile | 2046010108310242020
trade_no | String | Yes | 20 | Transaction ID of Pagsmile | 2018011908344902008
out_trade_no | String | Yes | 64 | Transaction ID of Merchant | 
trade_status | String | Yes | 20 | The status of that order | The current order status returned contains（TRADE_NORMAL、TRADE_CANCEL、RISK_CONTROL、TRADE_REFUSE）
passback_params | String | Yes | 255 | Temporarily not used, just pass in the blank | 
pay_channel | String | Yes | 255 | Corresponding payment channel | 
total_amount | String | Yes | 12 | The total amount of the order | 
currency | String | Yes | 3 | Currency | 
create_time | String | Yes | 20 | Recurring payment start time | 
update_time | String | Yes | 20 | Recurring payment status update time |
issue | String | Yes | 3 | Installment number |
version | String | Yes | 3 | Fixed as: 1.0 | 
sign_type | String | Yes | 32 | Fixed as: MD5 |  
sign | String | Yes | 32 | Refer to [Signature Algorithm](DriectSign)

>### Return Status  

For more details please refer to [Return Status and Error List](ReturnResult)

>## Return Result

Name | Type | Required | Max Length | Description | Sample
---  | ---  | ---      | ---      | ---  | ---
result | String | Yes | 32 | Return result | 'success':Success
