# Demo for JAVA

>## Integrated Interface

```
    public static void createOrder(HttpServletResponse response) throws IOException {
        String orderUrl = "{API URL}";

        String merchantNo = "replace with your own merchant_no.";
        String appId = "replace with your own APP id.";
        String appKey = "replace with your own APP key.";
        String timestamp = DateUtil.formatNow("yyyy-MM-dd HH:mm:ss");

        Map<String, String> params = new HashMap<>(20);
        params.put("merchant_no", merchantNo);
        params.put("app_id", appId);
        params.put("out_order_no", "#replace with your own order NO.");
        params.put("out_uid", "replace with your own user id.");
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
