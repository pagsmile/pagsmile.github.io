# 风控CPF校验接口说明

>## 接口链接

    URL: https://fcontrol.pagsmile.com/api/checkCpfInfo.json

>## 请求参数

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
ps_mid | String | Yes | 20 | pagsmile分配给商户的ID | 1024201708140012289
type | String | Yes | 2 | 请求包类型：1为基础校验，CPF号码和姓名校验；2为高级校验，校验包括姓名，性别，母亲姓名，生日信息。 | 1或2
cpf_no | String | Yes | 11 | 请求校验的CPF号码，不带特殊符号 | 
name | String | Yes | 255 | 请求校验的姓名
nameOfMom | String | Yes(type=2) | 255 | 请求校验的母亲的姓名（只在高级验证中必填）
birthday | String | Yes(type=2) | 10 | 请求校验的生日（只在高级验证中必填） | DD/MM/YYYY
gender | String | Yes(type=2) | 1 | 请求校验的性别（只在高级验证中必填） | （M \| F）
sign | String | Yes | 32 | 签名 | 

>## 返回结果

参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例值
---  | ---  | ---      | ---      | ---  | ---
code | String | Yes | 16 | 返回状态码 | 200:成功
info | String | Yes | 128 | 返回信息 | 

>## 错误码

错误码 | 描述 | 原因 | 解决方案
---  | ---  | ---  | ---
401 | SYSTEM_PARAM_ERROR | 包类型不正确 | 检查参数设置。
402 | SIGN_VERIFY_FAILURE | 签名错误 | 根据给定的规则设置签名，并确认参数sign字段设置正确。
502 | MERCHANT_ID_INVALID | 商户号不可用 | 检查参数中的商户号是否正确。
752 | CPF_NO_ISNULL | 请求CPF号码为空 | 检查参数设置。
924 | CPF_INFO_NOT_MATCH | CPF信息不匹配 | 
