---
title: DriectSignRsa
category: 交易平台
order: 26
language: cn
---
# 卡信息RSA签名算法

### 1. 签名说明
    
    为了保证在信用卡或者借记卡在传输中的安全性，将信用卡信息加密传输。

### 2. RSA密钥的获取

RSA密钥获取路径：商户平台(paccess.pagsmile.com)
     

### 3. 样例
    
1. 将需要加密的数据通过公钥加密，加密使用算法RSA/ECB/PKCS1Padding
    
    ```
     [
         'credit_card' => [
                    'brand' => 'visa',
                    'expirationDate' => '12/2020',
                    'holder' => 'Test User Name',
                    'number' => '0000000000000001',
                    'securityCode' => '123',
                ]
    ]
    
    ```
2. 通过公钥加密后

    ```
    [
        'credit_card' => [
                    'brand' => 'K9HjhLLP4aZu58ZaBF1a0IW6GK2njfzkL%2FeNXvtMroD%2FxI%2BCx9lsNf%2FLV3KZOG4ixTZ%2FfKOrArDEh3mUyR%2F91GouBtV3QznBFibgZRe4pEgyCgJtAwHustrHUJA%2Bg8o%2BPlXTNu0U5BntX8HaArdwn7rlVhvOT%2F%2BtxJ7LnHjrOWw%3D',
                    'expirationDate' => 'Qw2JiUkbgIRMfcxA7f3UM5Wq324qCXjLlxsmmKsYD%2Ftk%2FiFHmZG%2B4CY%2B2TgMFHbJwUNyExEz%2FPfpERclU%2BYjXluGrs1bUZjWkR6Lv5w5QodzRB29unucIQdyZd%2FK4dF8gR74zSNLqClFmJb9vm%2FLs4hIeNqUFWzlHp%2Bj1PdiuYE%3D',
                    'holder' => 'ii%2FxE8qc2De7hSm2YM%2BvDsUUlhYr7sZ2euuyopUmI6SmD8mxqefZezBMOq7k4TbbSaMKBzw9XfX1OkFPoY6%2FGY5SPPXZgd%2FkX8BPTsS%2BCU4A5ZMBJhH4LzU3Dau18ZO7%2BR8ywLtu17cNC7VRH2NHLZ3%2BSav0013EZdt85Bil3ak%3D',
                    'number' => 'ElyWxFc7%2FewEAgqKOEjdwryZnffHc4SiXNKrCGcMG%2F45e%2BrwRqS7cBjebmfIhUAE8Aw8GVr5Z1umtttZ8BRncEE2BzeBis376rH0wXHCezJLpAi5BjarQ%2B%2FEPZ67Un7GREmRALL2zYRzYDXv2y9cXdPOkaASUMxmn2FxhPmRBVU%3D',
                    'securityCode' => 'b9ko2u8CFLG%2F5c7FO%2Fw9PnRiuE6tLfyKxm4c8v6nfqk%2FmzfTFV2F08mgElhX1msgrBMZTe2NnZ2WPoMcb0ZuSqlAask%2FZkhmkYsBKjqBgrEXGp6wvLICisCXTDuqMd9p4xtHXEsR515a7yijfas2x0m%2BCN3ncQXA756ouRmSOrE%3D',
              ],
    ]
    ```

