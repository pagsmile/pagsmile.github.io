# 支付接口php demo

>## 集成接口下单demo

```
    public static void createOrder(HttpServletResponse response) throws IOException {
        String orderUrl = "https://testenv.pagsmile.com/pserver/gateway.json";

        String merchantNo = "";
        String appId = "";
        String appKey = "";
        String timestamp = DateUtil.formatNow("yyyy-MM-dd HH:mm:ss");

        Map<String, String> params = new HashMap<>(20);
        params.put("merchant_no", merchantNo);
        params.put("app_id", appId);
        params.put("out_order_no", RandomUtil.getRandom(8, RandomTypeEm.LETTER));
        params.put("out_uid", RandomUtil.getRandom(4, RandomTypeEm.NUMBER));
        params.put("subject", "subject");
        params.put("content", "content");
        params.put("order_amount", "10");
        params.put("currency", "BRL");
        params.put("charset", "utf-8");
        params.put("timestamp", timestamp);
        params.put("version", "1.0");
        params.put("timeout_express", "2h");
        params.put("passback_params", "passback_params");
        params.put("notify_url", "");
        params.put("return_url", "");
        params.put("sign_type", "MD5");
        String sign = SignUtil.md5Sign(params, appKey);
        params.put("sign", sign);

        HttpUrl url = HttpUrl.get(orderUrl);

        for (Map.Entry<String, String> entry : params.entrySet()) {
            url = url.newBuilder().addQueryParameter(entry.getKey(), entry.getValue()).build();
        }

        response.sendRedirect(url.toString());
    }
```
