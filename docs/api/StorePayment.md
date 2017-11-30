/v1/StorePayment/Get
--------------------

取得商店目前有設定使用的pay type

+-------------+-------------------------------------------------------------+
| Attribute   | Value                                                       |
+=============+=============================================================+
| API Name    | 取得 Pay Type 資訊 (/StorePayment/Get)                      |
+-------------+-------------------------------------------------------------+
| API Desc    | 取得商店目前有設定使用的pay type                            |
+-------------+-------------------------------------------------------------+
| Version     | 1                                                           |
+-------------+-------------------------------------------------------------+
| Request URI | https://tw.ews.mall.yahooapis.com/stauth/v1/StorePayment/Get|
|             |                      OR                                     |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/StorePayment/Get |
+-------------+-------------------------------------------------------------+
| Change Log  | *                                                           |
+-------------+-------------------------------------------------------------+

### Response fields

+---------------+-------------------------------+
| Field         | Description                   |
+===============+===============================+
| StoreId       | 商店代號 (string)             |
+---------------+-------------------------------+
| PayTypeList   | 包含PayType List，屬性：      |
|               |                               |
|               | * Count：資料筆數             |
+---------------+-------------------------------+
| PayType       | 包含一筆PayType的資料，屬性： |
|               |                               |
|               | * Id ：付款方式代號           |
+---------------+-------------------------------+
| Name          | 付款方式名稱 (string)         |
+---------------+-------------------------------+
| UserDefaultOn | 套用全店商品 (string)         |
|               |                               |
|               | on/off                        |
+---------------+-------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "PayTypeList":{
      "@Count":6,
      "PayType":[
        {
          "@Id":1,
          "Name":"ATM \u8f49\u5e33",
          "UserDefaultOn":"off"
        },
        {
          "@Id":2,
          "Name":"\u4fe1\u7528\u5361\u4e00\u6b21\u4ed8\u6e05",
          "UserDefaultOn":"off"
        },
        {
          "@Id":4,
          "Name":"\u4fe1\u7528\u53613\u671f\u96f6\u5229\u7387",
          "UserDefaultOn":"off"
        },
        {
          "@Id":6,
          "Name":"\u4fe1\u7528\u536112\u671f\u96f6\u5229\u7387",
          "UserDefaultOn":"on"
        },
        {
          "@Id":8,
          "Name":"\u4fe1\u7528\u53613\u671f",
          "UserDefaultOn":"off"
        },
        {
          "@Id":11,
          "Name":"7-11\u53d6\u8ca8\u4ed8\u6b3e",
          "UserDefaultOn":"on"
        }
      ]
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
  <PayTypeList Count="6">
    <PayType Id="1">
      <Name><![CDATA[ATM 轉帳]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
    </PayType>
    <PayType Id="2">
      <Name><![CDATA[信用卡一次付清]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
    </PayType>
    <PayType Id="4">
      <Name><![CDATA[信用卡3期零利率]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
    </PayType>
    <PayType Id="6">
      <Name><![CDATA[信用卡12期零利率]]></Name>
      <UserDefaultOn>on</UserDefaultOn>
    </PayType>
    <PayType Id="8">
      <Name><![CDATA[信用卡3期]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
    </PayType>
    <PayType Id="11">
      <Name><![CDATA[7-11取貨付款]]></Name>
      <UserDefaultOn>on</UserDefaultOn>
    </PayType>
  </PayTypeList>
</Response>
```

### Errors

+-----------+-----------------------+
| ErrorCode | ErrorMessage          |
+===========+=======================+
| 99        | Internal server error |
+-----------+-----------------------+

