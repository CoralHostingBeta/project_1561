/v1/StoreCategory/Get
---------------------

取得此Store的自訂category

+-------------+--------------------------------------------------------------+
| Attribute   | Value                                                        |
+=============+==============================================================+
| API Name    | 取特定 Category 資訊 (/StoreCategory/Get)                    |
+-------------+--------------------------------------------------------------+
| API Desc    | 取得此 Store 的自定 Category                                 |
+-------------+--------------------------------------------------------------+
| Version     | 1                                                            |
+-------------+--------------------------------------------------------------+
| Request URI | https://tw.ews.mall.yahooapis.com/stauth/v1/StoreCategory/Get|
|             |                      OR                                      |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/StoreCategory/Get |
+-------------+--------------------------------------------------------------+
| Change Log  | *                                                            |
+-------------+--------------------------------------------------------------+

### Response fields

+-------------------+--------------------------------------+
| Field             | Description                          |
+===================+======================================+
| StoreCategoryList | 包含此商店的Category List，屬性：    |
|                   |                                      |
|                   | * Count：資料筆數                    |
+-------------------+--------------------------------------+
| StoreCategory     | 包含一筆商店的Category的資料，屬性： |
|                   |                                      |
|                   | * Id ：分類代號                      |
+-------------------+--------------------------------------+
| Path              | 分類路徑名稱 (string)                |
|                   |                                      |
|                   | ex：家具 > 櫥櫃 > 收納櫃             |
+-------------------+--------------------------------------+
| IsDisplay         | 是否顯示 (string)                    |
|                   |                                      |
|                   | True/Flase                           |
+-------------------+--------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "StoreCategoryList":{
      "@Count":5,
      "StoreCategory":[
        {
          "Id":2,
          "Path":"\u5927\u5206\u985e > \u4e2d\u5206\u985e\u4e00",
          "IsDisplay":"true"
        },
        {
          "Id":6,
          "Path":"\u5927\u5206\u985e > \u4e2d\u5206\u985e\u4e8c > \u5c0f\u5206\uff11",
          "IsDisplay":"true"
        },
        {
          "Id":7,
          "Path":"\u5927\u5206\u985e > \u4e2d\u5206\u985e\u4e8c > \u5c0f\u5206\uff12",
          "IsDisplay":"false"
        },
        {
          "Id":3,
          "Path":"\u5927\u5206\u985e\u4e8c",
          "IsDisplay":"true"
        },
        {
          "Id":8,
          "Path":"\u5927\u5206\u985e\u4e09 > \u4e2d\u5206\u985e\u4e09",
          "IsDisplay":"true"
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
  <StoreCategoryList Count="5">
    <StoreCategory>
      <Id>2</Id>
      <Path><![CDATA[大分類 > 中分類一]]></Path>
      <IsDisplay>true</IsDisplay>
    </StoreCategory>
    <StoreCategory>
      <Id>6</Id>
      <Path><![CDATA[大分類 > 中分類二 > 小分１]]></Path>
      <IsDisplay>true</IsDisplay>
    </StoreCategory>
    <StoreCategory>
      <Id>7</Id>
      <Path><![CDATA[大分類 > 中分類二 > 小分２]]></Path>
      <IsDisplay>false</IsDisplay>
    </StoreCategory>
    <StoreCategory>
      <Id>3</Id>
      <Path><![CDATA[大分類二]]></Path>
      <IsDisplay>true</IsDisplay>
    </StoreCategory>
    <StoreCategory>
      <Id>8</Id>
      <Path><![CDATA[大分類三 > 中分類三]]></Path>
      <IsDisplay>true</IsDisplay>
    </StoreCategory>
  </StoreCategoryList>
</Response>
```

### Errors

+-----------+-----------------------+
| ErrorCode | ErrorMessage          |
+===========+=======================+
| 99        | Internal server error |
+-----------+-----------------------+

