>### 返回订单状态一览  

状态码 | 状态说明
:--- | ---:
WAIT_BUYER_PAY | 等待付款
TRADE_SUCCESS | 成功
TRADE_RISK_CONTROL | 支付风控处理中（2h-2d审核）
TRADE_PROCESSING | 订单等待后续处理
TRADE_REFUND | 退款
TRADE_REFUND_PRT | 部分退款
TRADE_REFUND_MER | 退款
REFUND_IN_VERIFY | 退款信息验证中
REFUND_IN_PROCESS | 退款中
REFUND_REFUSED | 退款拒绝
REFUND_REVERSED | 退款撤销
TRADE_CHARGEBACK | 拒付
CHARGEBACK_REVERSED | 拒付驳回
TRADE_REFUSED | 付款被拒绝
TRADE_CANCEL | 取消
TRADE_DISPUTE | 争议
DISPUTE_REVERSED | 争议取消
FRAUD_REFUSED | 风控拒绝
PAID_MAJOR | 收款金额大于实际金额（仅boleto）
PAID_MINOR | 收款金额小于实际金额（仅boleto）

>### 返回错误码一览  

错误码 | 错误描述 
:----  | :--- 
200 | SUCCESS
300 | WARNING
400 |	SYSTEM_ERROR
401 |	SYSTEM_PARAM_ERROR
402 |	SIGN_VERIFY_FAILURE
403	| SIGN_ISNULL
404	| SIGN_TYPE_ERROR
405	| SIGN_TYPE_ISNULL
501	| MERCHANT_ID_NOT_EXIST
502	| MERCHANT_ID_INVALID
507	| MERCHANT_ID_NOT_ACTIVE
508	| MERCHANT_STATUS_ISLOCK
550	| SINGLE_DAY_PAY_LIMIT
551	| IP_REQUEST_TOO_FAST_LIMIT
601	| APP_ID_NOT_EXIST
602	| APP_ID_INVALID
603	| APP_ID_ISNULL
604	| APP_STATUS_ISLOCK
750	| CPF_INFO_NOT_EXIST
752	| CPF_NO_ISNULL
759	| EMAIL_ISNULL
760	| PHONE_ISNULL
761	| BANK_ILLEGAL
762 | AMOUNT ILLEGAL
763 | ZIP_CODE_IS_NULL
764 | ZIP_CODE_ILLEGAL
766 | IDENTIFICATION_IS_NULL
767 | TYPE_ISNULL
801	| TRADENO_NOT_EXIST
802	| TRADENO_ISNULL
803	| TRADE_CURRENCY_ISNULL
804	| TRADE_ALREADY_SUCCESS
805	| TRADE_STATUS_EXCEPTION
806	| TRADE_TIMEOUT_CLOSE
807	| TRADE_STATUS_ISNULL
810	| BOLETO_SYSTEM_BUSY
811	| ONLINEBANK_SYSTEM_BUSY
812	| REJECTED_BY_BANK
813	| METHOD_NOT_OPEN
814	| TRADE_INS_OVER
815	| ORDER_IS_NOT_EXIST
816	| BANK_NOT_CREATE_ORDER
817	| UPLOAD_FAILD
818 | FILE_SIZE_LIMIT
819 | FILE_TYPE_NOT_SUPPORT
910	| CARD_NO_ISNULL
911	| CARD_TYPE_ISNULL
912	| CARD_IS_BLACK_CARD
913	| CARD_USER_INFO_NOT_MATCH
914	| CARD_USER_USER_TO_MANY
915	| CARD_TRADE_TOO_FREQUENT
916	| CARD_TRADE_TOO_LARGE
917	| CARD_TRADE_IP_LIMIT
918	| CARD_TRADE_FREQUENT_PER_M
922	| CPF_IS_BLACK_CPF
923	| CPF_IS_VERIFYING
924	| CPF_INFO_NOT_MATCH
930	| USERNAME_ISNULL
931	| USER_IS_BLACK_USER
932	| USER_USE_CARD_TO_MANY
935	| MUID_TRADE_IP_LIMIT
936	| MUID_TRADE_FREQUENT_PER_M
937	| MUID_CPF_INFO_NOT_MATCH
938	| USERNAME_ILLEGAL
bank-1 | Unauthorized transaction. Referred transaction.
bank-2 | Unauthorized transaction. Referred transaction.
bank-3 | Transaction not allowed. Error in registering the establishment code in the TEF configuration file
bank-4 | Unauthorized transaction. Card blocked by issuing bank.
bank-5 | Unauthorized transaction. Defaulting card (Do not honor).
bank-6 | Unauthorized transaction. Card canceled.
bank-7 | Transaction declined. Hold special condition card
bank-8 | Unauthorized transaction. Invalid security code.
bank-11	| Successfully authorized transaction for card issued abroad
bank-12	| Invalid transaction, card error.
bank-13	| Transaction not allowed. Invalid transaction value.
bank-14	| Unauthorized transaction. Invalid Card
bank-15	| Issuing bank unavailable or non-existent.
bank-19	| Redo the transaction or try again later.
bank-21 | Cancellation not done. Non-localized transaction.
bank-22 | Invalid installment. Invalid number of installments.
bank-23 | Unauthorized transaction. Invalid installment value.
bank-24 | Invalid number of installments.
bank-25 | Request for authorization did not send card number
bank-28 | File temporarily unavailable.
bank-30 | Unauthorized transaction. Decline Message
bank-39 | Unauthorized transaction. Error at the issuing bank.
bank-41 | Unauthorized transaction. Card locked for loss.
bank-43 | Unauthorized transaction. Card locked for theft.
bank-51 | Unauthorized transaction. Limit exceeded/no balance.
bank-52 | Card with invalid control digit.
bank-53 | Transaction not allowed. Invalid Savings card
bank-54 | Unauthorized transaction. Expired card
bank-55 | Unauthorized transaction. Invalid password
bank-57 | Transaction not allowed for the card
bank-58 | Transaction not allowed. Invalid payment option.
bank-59 | Unauthorized transaction. Suspected fraud.
bank-60 | Unauthorized transaction.
bank-61 | Issuing bank unavailable.
bank-62 | Unauthorized transaction. Card restricted for home use
bank-63 | Unauthorized transaction. Security breach
bank-64 | Unauthorized transaction. Value below the minimum required by the issuing bank.
bank-65 | Unauthorized transaction. Exceeded the number of transactions for the card.
bank-67 | Unauthorized transaction. Card locked for shopping today.
bank-70 | Unauthorized transaction. Limit exceeded/no balance.
bank-72 | Cancellation not done. Not enough available balance for cancellation.
bank-74 | Unauthorized transaction. The password is expired.
bank-75 | Password locked. Exceeded card attempts.
bank-76 | Cancellation not done. Issuer bank did not locate the original transaction
bank-77 | Cancellation not done. The original transaction was not found
bank-78 | Unauthorized transaction. Locked card first use.
bank-80 | Unauthorized transaction. Divergence on transaction/payment date.
bank-82 | Unauthorized transaction. Invalid card.
bank-83 | Unauthorized transaction. Error in password control
bank-85 | Transaction not allowed. Operation failed.
bank-86 | Transaction not allowed. Operation failed.
bank-89 | Transaction error.
bank-90 | Transaction not allowed. Operation failed.
bank-91 | Unauthorized transaction. Issuing bank temporarily unavailable.
bank-92 | Unauthorized transaction. Communication time exceeded.
bank-93 | Unauthorized transaction. Rule violation - Possible error in register.
bank-96 | Processing failed.
bank-97 | Value not allowed for this transaction.
bank-98 | System/communication unavailable.
bank-99 | System/communication unavailable.
bank-999 | System/communication unavailable.
bank-AA | Time Exceeded
bank-AC | Transaction not allowed. Debit card being used as credit. Use the debit function.
bank-AE | Try later
bank-AF | Transaction not allowed. Operation failed.
bank-AG | Transaction not allowed. Operation failed.
bank-AH | Transaction not allowed. Credit card being used as debit. Use the credit function.
bank-AI | Unauthorized transaction. Authentication was not performed.
bank-AJ | Transaction not allowed. Credit or debit transaction in an operation that allows only Private Label. Try again by selecting the Private Label option.
bank-AV	| Unauthorized transaction. Invalid data
bank-BD	| Transaction not allowed. Operation failed.
bank-BL	| Unauthorized transaction. Daily limit exceeded.
bank-BM	| Unauthorized transaction. Invalid card
bank-BN	| Unauthorized transaction. Card or account locked.
bank-BO	| Transaction not allowed. Operation failed.
bank-BP	| Unauthorized transaction. Non-existent checking account.
bank-BV	| Unauthorized transaction. Expired card
bank-CF	| Unauthorized transaction.C79:J79 Data validation failed.
bank-CG	| Unauthorized transaction. Data validation failed.
bank-DA	| Unauthorized transaction. Data validation failed.
bank-DF	| Transaction not allowed. Invalid card or card failure.
bank-DM	| Unauthorized transaction. Limit exceeded/no balance.
bank-DQ	| Unauthorized transaction. Data validation failed.
bank-DS	| Transaction not allowed for the card
bank-EB	| Unauthorized transaction. Daily limit exceeded.
bank-EE	| Transaction not allowed. Installment value below the minimum allowed.
bank-EK	| Transaction not allowed for the card
bank-FA	| Unauthorized transaction.
bank-FC	| Unauthorized transaction. Call the Issuer
bank-FD	| Transaction declined. Hold special condition card
bank-FE	| Unauthorized transaction. Divergence on transaction/payment date.
bank-FF	| Cancellation OK
bank-FG	| Unauthorized transaction. Call AmEx.
bank-FG	| Call 08007285090
bank-GA	| Wait for contact
bank-HJ	| Transaction not allowed. Invalid operation code.
bank-IA	| Transaction not allowed. Invalid operation indicator.
bank-JB	| Transaction not allowed. Invalid operation value.
bank-KA	| Transaction not allowed. Data validation failed.
bank-KB	| Transaction not allowed. Incurred option selected.
bank-KE	| Unauthorized transaction. Data validation failed.
bank-N7	| Unauthorized transaction. Invalid security code.
bank-R1	| Unauthorized transaction. Default card (Do not honor).
bank-U3	| Transaction not allowed. Data validation failed.
bank-GD	| Transaction not allowed.
mbank-400 | Invalid transaction_amount - 4037: Invalid transaction_amount
