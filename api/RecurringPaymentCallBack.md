># 订阅付费回调通知

订阅付费开启后，pagsmile会把相关支付结果和用户信息发送给商户，商户需要接收处理，并返回应答。

对后台通知交互时，如果pagsmile收到商户的应答不是成功或超时，pagsmile认为通知失败，并会通过一定的策略定期重新发起通知，尽可能提高通知的成功率，但pagsmile不保证通知最终能成功。 （通知频率为4/10/10/30/60/120，单位：分钟）

注意：同样的通知可能会多次发送给商户系统。商户系统必须能够正确处理重复的通知。
推荐的做法是，当收到通知进行处理时，首先检查对应业务数据的状态，判断该通知是否已经处理过，如果没有处理过再进行处理，如果处理过直接返回结果成功。在对业务数据进行状态检查和处理之前，要采用数据锁进行并发控制，以避免函数重入造成的数据混乱。

特别提醒：商户系统对于支付结果通知的内容一定要做签名验证,并校验返回的订单金额是否与商户侧的订单金额一致，防止数据泄漏导致出现“假通知”，造成资金损失。
订阅付费的订单回调通知包括两种：1.订阅主订单的回调通知（详见：[通知参数](#dasd)） 2.订阅子订单的回调通知（详见：[订单回调通知](CallBack)）


># 接口链接

该链接是通过【下单API】中提交的参数notify_url设置，如果链接无法访问，商户将无法接收到pagsmile通知。

通知url必须为直接可访问的url，不能携带参数。示例：notify_url：“https://callback.pagsmile.com/pay/callback.json”

>## 通知参数<span id="dasd"></span>


参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
subscription_no | String | Yes | 20 | pagsmile订阅付费的ID | 2046010108310242020
trade_no | String | Yes | 20 | pagsmile订阅付费生成的交易ID | 2018011908344902008
out_trade_no | String | Yes | 64 | 商户请求下单时发送的对应商户的交易ID | 
trade_status | String | Yes | 20 | 返回的订单状态 | 目前返回的订单状态包含（TRADE_NORMAL、TRADE_CANCEL、RISK_CONTROL、TRADE_REFUSE）
passback_params | String | Yes | 255 | 暂时没有用到，传空即可 | 
pay_channel | String | Yes | 255 | 对应的支付渠道 | 
total_amount | String | Yes | 12 | 订单总金额 | 
currency | String | Yes | 3 | 币种 | 
create_time | String | Yes | 20 | 订阅付费开启时间
update_time | String | Yes | 20 | 订阅付费状态更新时间
issue | String | Yes | 3 | 订阅付费当前期数
version | String | Yes | 3 | 固定为：1.0 即可 | 
sign_type | String | Yes | 32 | 固定为：MD5 即可 |  
sign | String | Yes | 32 | 参照[签名算法](DriectSign)

>### 返回状态对应关系  

更详细列表请参照[返回状态和错误一览](ReturnResult)

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
result | String | Yes | 32 | 返回结果 | 'success':成功
