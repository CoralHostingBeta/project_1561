/v1/StoreShipping/Get
---------------------

取得商店目前有設定使用的shipping type

+-------------+--------------------------------------------------------------+
| Attribute   | Value                                                        |
+=============+==============================================================+
| API Name    | 取特定 Shipping Type 資訊 (StoreShipping/Get)                |
+-------------+--------------------------------------------------------------+
| API Desc    | 取得商店目前有設定使用的shipping type                        |
+-------------+--------------------------------------------------------------+
| Version     | 1                                                            |
+-------------+--------------------------------------------------------------+
| Request URI | https://tw.ews.mall.yahooapis.com/stauth/v1/StoreShipping/Get|
|             |                      OR                                      |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/StoreShipping/Get |
+-------------+--------------------------------------------------------------+
| Change Log  | *                                                            |
+-------------+--------------------------------------------------------------+

### Response fields

+------------------+------------------------------------+
| Field            | Description                        |
+==================+====================================+
| ShippingTypeList | 包含ShippingType List，屬性：      |
|                  |                                    |
|                  | * Count：資料筆數                  |
+------------------+------------------------------------+
| ShippingType     | 包含一筆ShoppingType的資料，屬性： |
|                  |                                    |
|                  | * Id ：物流方式代號                |
+------------------+------------------------------------+
| Name             | 物流方式名稱 (string)              |
+------------------+------------------------------------+
| UserDefaultOn    | 套用全店商品 (string)              |
|                  |                                    |
|                  | on/off                             |
+------------------+------------------------------------+
| FeeType          | 運費類型 (string)                  |
|                  |                                    |
|                  | * Free/PriceLine/Fixed             |
|                  | * Free:免運費                      |
|                  | * PriceLine:一價區隔制             |
|                  | * Fixed:固定運費制                 |
+------------------+------------------------------------+
| Desc             | 運費類型說明 (string)              |
|                  |                                    |
|                  | * 免運費                           |
|                  | * 購物未滿XX元，收XX元運費         |
|                  | * 每筆訂單收固定運費XX元           |
+------------------+------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "ShippingTypeList":{
      "@Count":3,
      "ShippingType":[
        {
          "@Id":1,
          "Name":"\u90f5\u5bc4",
          "UserDefaultOn":"on",
          "FeeType":"Fixed",
          "Desc":false
        },
        {
          "@Id":2,
          "_Name":"\u8ca8\u904b \/ \u5b85\u914d",
          "UserDefaultOn":"off",
          "FeeType":"PriceLine",
          "Desc":false
        },
        {
          "@Id":3,
          "Name":"\u4f4e\u6eab\u914d\u9001",
          "UserDefaultOn":"off",
          "FeeType":"PriceLine",
          "Desc":false
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
  <ShippingTypeList Count="3">
    <ShippingType Id="1">
      <Name><![CDATA[郵寄]]></Name>
      <UserDefaultOn>on</UserDefaultOn>
      <FeeType>Fixed</FeeType>
      <Desc><![CDATA[false]]></Desc>
    </ShippingType>
    <ShippingType Id="2">
      <Name><![CDATA[貨運 / 宅配]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
      <FeeType>PriceLine</FeeType>
      <Desc><![CDATA[false]]></Desc>
    </ShippingType>
    <ShippingType Id="3">
      <Name><![CDATA[低溫配送]]></Name>
      <UserDefaultOn>off</UserDefaultOn>
      <FeeType>PriceLine</FeeType>
      <Desc><![CDATA[false]]></Desc>
    </ShippingType>
  </ShippingTypeList>
</Response>
```

### Errors

+-----------+-----------------------+
| ErrorCode | ErrorMessage          |
+===========+=======================+
| 99        | Internal server error |
+-----------+-----------------------+

