/v1/Exchange/Query
------------------

換貨單查詢，可依據不同的條件查詢換貨單列表

### Request parameters

+----------------+--------------------+------------------------------------+
| Parameter      | Value              | Description                        |
+================+====================+====================================+
| ExchangeStatus | string(Require)    | 換貨單狀態                         |
|                |                    |                                    |
|                |                    | * All:全部                         |
|                |                    | * NonConfirm:未確認                |
|                |                    | * NonClose:未結案                  |
|                |                    | * Close:結案                       |
+----------------+--------------------+------------------------------------+
| DateType       | string(20/Require) | 日期條件                           |
|                |                    |                                    |
|                |                    | * ExchangeCreateDate:換貨單建立日  |
|                |                    | * ExchangeConfirmDate:換貨單確認日 |
+----------------+--------------------+------------------------------------+
| StartDate      | Date(Require)      | 起始日期                           |
|                |                    |                                    |
|                |                    | (yyyy/mm/dd)                       |
+----------------+--------------------+------------------------------------+
| EndDate        | Date(Require)      | 迄止日期                           |
|                |                    |                                    |
|                |                    | (yyyy/mm/dd)                       |
|                |                    |                                    |
|                |                    | EndDate-StartDate要小於等於7天     |
+----------------+--------------------+------------------------------------+
| Position       | int(Require)       | 由第幾筆開始拿資料                 |
+----------------+--------------------+------------------------------------+
| Count          | int(Require)       | 資料筆數                           |
|                |                    |                                    |
|                |                    | Count=1~100                        |
+----------------+--------------------+------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/Query?ExchangeStatus=All&DateType=ExchangeCreateDate&ExchangeConfirmDate&StartDate=2011/01/01&EndDate=2011/01/02&Position=1&Count=1&Format=xml
                                                                            OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/Query?ExchangeStatus=All&DateType=ExchangeCreateDate&ExchangeConfirmDate&StartDate=2011/01/01&EndDate=2011/01/02&Position=1&Count=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------+--------------------------------------------+
| Field           | Description                                |
+=================+============================================+
| TransactionList | 包含符合查詢條件的Transaction List，屬性： |
|                 |                                            |
|                 | * Count：資料筆數                          |
+-----------------+--------------------------------------------+
| TotalCount      | 符合查詢條件的總資料筆數                   |
+-----------------+--------------------------------------------+
| Transaction     | 包含一筆Transaction的資料，屬性：          |
|                 |                                            |
|                 | * Id：交易序號                             |
+-----------------+--------------------------------------------+
| Order           | 包含一筆Order的資料，屬性：                |
|                 |                                            |
|                 | * Id：訂單編號                             |
+-----------------+--------------------------------------------+
| ExchangeId      | 換貨單序號                                 |
+-----------------+--------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "TransactionList": {
      "@Count": 2,
      "@TotalCount": 10,
      "Transaction": [
        {
          "@Id": "12345",
          "Order": [
            {
              "@Id": "YM1234567",
              "Exchange": {"@Id": "EX1234546"}
            },
            {
              "@Id": "YM1234568",
              "Exchange": {"@Id": "EX1234547"}
            },
            {
              "@Id": "YM1234569",
              "Exchange": {"@Id": "EX1234510"}
            }
          ]
        },
        {
          "@Id": "12346",
          "Order": [
            {
              "@Id": "YM1234511",
              "Exchange": {"@Id": "EX1234501"}
            },
            {
              "@Id": "YM1234512",
              "Exchange": {"@Id": "EX1234502"}
            },
            {
              "@Id": "YM1234513",
              "Exchange": {"@Id": "EX1234503"}
            }
          ]
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
      <TransactionList Count="2" TotalCount="10">
            <Transaction Id="12345">
                  <Order Id="YM1234567">
                        <Exchange Id="EX1234546"></Exchange>
                  </Order>
                  <Order Id="YM1234568">
                        <Exchange Id="EX1234547"></Exchange>
                  </Order>
                  <Order Id="YM1234569">
                        <Exchange Id="EX1234510"></Exchange>
                  </Order>
            </Transaction>
            <Transaction Id="12346">
                  <Order Id="YM1234511">
                        <Exchange Id="EX1234501"></Exchange>
                  </Order>
                  <Order Id="YM1234512">
                        <Exchange Id="EX1234502"></Exchange>
                  </Order>
                  <Order Id="YM1234513">
                        <Exchange Id="EX1234503"></Exchange>
                  </Order>
            </Transaction>
      </TransactionList>
</Response>
```

### Errors

---

/v1/Exchange/Get
----------------

取得換貨單明細資料

### Request parameters

+------------+-----------------+-------------+
| Parameter  | Value           | Description |
+============+=================+=============+
| ExchangeId | string(Require) | 換貨單序號  |
+------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/Get?ExchangeId=212342&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/Get?ExchangeId=212342&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------------+------------------+
| Field                 | Description      |
+=======================+==================+
| ExchangeId            | 換貨單序號       |
+-----------------------+------------------+
| ExchangeCreateDate    | 換貨單建立日期   |
|                       |                  |
|                       | (yyyy/mm/dd)     |
+-----------------------+------------------+
| ExchangeReason        | 換貨原因         |
|                       |                  |
|                       | *                |
+-----------------------+------------------+
| ExchangeRemark        | 換貨原因備註     |
+-----------------------+------------------+
| SellerRemark          | 店家備註         |
+-----------------------+------------------+
| ProductId             | 商品編號         |
+-----------------------+------------------+
| CustomizedProductId   | 自訂貨號         |
+-----------------------+------------------+
| ProductName           | 商品名稱         |
+-----------------------+------------------+
| Spec                  | 商品規格         |
+-----------------------+------------------+
| ExchangePickupName    | 換貨取件姓名     |
+-----------------------+------------------+
| ExchangePickupMobile  | 換貨取件手機     |
+-----------------------+------------------+
| ExchangePickupPhone   | 換貨取件電話     |
+-----------------------+------------------+
| ExchangePickupZipcode | 換貨取件郵遞區號 |
+-----------------------+------------------+
| ExchangePickupAddress | 換貨取件地址     |
+-----------------------+------------------+
| ExchangeConfirmDate   | 換貨確認日       |
|                       |                  |
|                       | (yyyy/mm/dd)     |
+-----------------------+------------------+
| ExchangeCloseDate     | 換貨結案日       |
|                       |                  |
|                       | (yyyy/mm/dd)     |
+-----------------------+------------------+
| ExchangeCloseReason   | 換貨結案原因     |
+-----------------------+------------------+
| ExchangeCloseRemark   | 換貨結案備註     |
+-----------------------+------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Exchange": {
      "@Id": "EX123456",
      "ExchangeCloseDate": "2010/11/13",
      "ExchangeConfirmDate": "2010/11/12",
      "ExchangeCreateDate": "2010/11/12",
      "ExchangePickupZipcode": "100",
      "ProductId": "p12344556",
      "SpecId": "1",
      "_CustomizedProductId": "A-123456",
      "_ExchangeCloseReason": "\u5df2\u8655\u7406",
      "_ExchangeCloseRemark": "\u5df2\u8655\u7406",
      "_ExchangePickupAddress": "\u53f0\u5317\u5e02\u58eb\u6797\u534010000\u865f",
      "_ExchangePickupName": "\u738b\u5927\u660e",
      "_ExchangePickupMobile": "\u63db\u8ca8\u53d6\u4ef6\u624b\u6a5f",
      "_ExchangePickupPhone": "02-22222222",
      "_ExchangeReason": "\u4e0d\u559c\u6b61\uff0csize\u4e0d\u5408",
      "_ExchangeRemark": "size \u4e0d\u5408",
      "_ProductName": "\u5167\u8863",
      "_SellerRemark": "XL\u63dbM",
      "_Spec": "\u767d\u8272"
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Exchange Id="EX123456">
            <ExchangeCreateDate>2010/11/12</ExchangeCreateDate>
            <ExchangeReason>                  <![CDATA[不喜歡，size不合]]>
            </ExchangeReason>
            <ExchangeRemark>
                  <![CDATA[size 不合]]>
            </ExchangeRemark>
            <SellerRemark>
                  <![CDATA[XL換M]]>
            </SellerRemark>
            <ProductId>p12344556</ProductId>
            <SpecId>1</SpecId>
            <CustomizedProductId>
                  <![CDATA[A-123456]]>
            </CustomizedProductId>
            <ProductName>
                  <![CDATA[內衣]]>
            </ProductName>
            <Spec>
                  <![CDATA[內衣]]>
            </Spec>
            <ExchangePickupName>
                  <![CDATA[王大明]]>
            </ExchangePickupName>
            <ExchangePickupMobile>
                  <![CDATA[0900-999999]]>
            </ExchangePickupMobile>            
            <ExchangePickupPhone>
                  <![CDATA[02-22222222]]>
            </ExchangePickupPhone>
            <ExchangePickupZipcode>100</ExchangePickupZipcode>
            <ExchangePickupAddress>
                  <![CDATA[台北市士林區10000號]]>
            </ExchangePickupAddress>
            <ExchangeConfirmDate>2010/11/12</ExchangeConfirmDate>
            <ExchangeCloseDate>2010/11/13</ExchangeCloseDate>
            <ExchangeCloseReason>
                  <![CDATA[已處理]]>
            </ExchangeCloseReason>
            <ExchangeCloseRemark>
                  <![CDATA[已處理]]>
            </ExchangeCloseRemark>
      </Exchange>
</Response>
```

### Errors

---

/v1/Exchange/Confirm
--------------------

執行換貨確認

### Request parameters

+------------+-----------------+-------------+
| Parameter  | Value           | Description |
+============+=================+=============+
| ExchangeId | string(Require) | 換貨單序號  |
+------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/Confirm?ExchangeId=212342&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/Confirm?ExchangeId=212342&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+---------------------+--------------+
| Field               | Description  |
+=====================+==============+
| ExchangeConfirmDate | 換貨確認日   |
|                     |              |
|                     | (yyyy/mm/dd) |
+---------------------+--------------+
| ErrorCode           | 錯誤代碼     |
+---------------------+--------------+
| ErrorMessage        | 錯誤訊息     |
+---------------------+--------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Exchange": {
      "@Id": "EX123456",
      "ExchangeConfirmDate": "2010/11/12"
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Exchange Id="EX123456">
            <ExchangeConfirmDate>2010/11/12</ExchangeConfirmDate>
      </Exchange>
</Response>
```

### Errors

+-----------+------------------------------------------+
| ErrorCode | ErrorMessage                             |
+===========+==========================================+
| 2201      | 該換貨單已結案                           |
+-----------+------------------------------------------+
| 2202      | 該換貨單已確認過                         |
+-----------+------------------------------------------+
| 2204      | 無資料被影響                             |
+-----------+------------------------------------------+
| 2921      | 換貨單確認成功，但寄發換貨確認通知信失敗 |
+-----------+------------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Exchange/Close
------------------

執行換貨結案,表示完成換貨作業

### Request parameters

+----------------------+------------------+--------------------------------------------+
| Parameter            | Value            | Description                                |
+======================+==================+============================================+
| ExchangeId           | string(Require)  | 換貨單序號                                 |
+----------------------+------------------+--------------------------------------------+
| ExchangeCloseReason  | int(Require)     | 換貨結案原因                               |
|                      |                  |                                            |
|                      |                  | 請參閱/Exchange/GetCloseReasonList填入代碼 |
+----------------------+------------------+--------------------------------------------+
| ExchangeCloseRemark  | string(Optional) | 換貨結案備註                               |
+----------------------+------------------+--------------------------------------------+
| ShippingSupplierCode | int(Optional)    | 新品送出之物流商代碼                       |
+----------------------+------------------+--------------------------------------------+
| ShippingNumber       | String(Optional) | 新品送出之貨運單號                         |
+----------------------+------------------+--------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/Close?ExchangeId=212342&ExchangeCloseReason=2&ExchangeCloseRemark=NoComment&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/Close?ExchangeId=212342&ExchangeCloseReason=2&ExchangeCloseRemark=NoComment&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-------------------+--------------+
| Field             | Description  |
+===================+==============+
| ExchangeCloseDate | 換貨結案日   |
|                   |              |
|                   | (yyyy/mm/dd) |
+-------------------+--------------+
| ErrorCode         | 錯誤代碼     |
+-------------------+--------------+
| ErrorMessage      | 錯誤訊息     |
+-------------------+--------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Exchange": {
      "@Id": "EX123456",
      "ExchangeCloseDate": "2010/11/13"
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Exchange Id="EX123456">
            <ExchangeCloseDate>2010/11/13</ExchangeCloseDate>
      </Exchange>
</Response>
```

### Errors

+-----------+------------------------------------------------+
| ErrorCode | ErrorMessage                                   |
+===========+================================================+
| 2301      | 該換貨單已結案                                 |
+-----------+------------------------------------------------+
| 2302      | 該換貨單尚未確認                               |
+-----------+------------------------------------------------+
| 2304      | 無資料被影響                                   |
+-----------+------------------------------------------------+
| 2305      | 換貨結案原因不存在                             |
+-----------+------------------------------------------------+
| 2306      | 物流商代碼不存在                               |
+-----------+------------------------------------------------+
| 2931      | 換貨單已結案，但找不到店家資訊，無法新增問題單 |
+-----------+------------------------------------------------+
| 2932      | 其他錯誤                                       |
+-----------+------------------------------------------------+
| 2933      | 換貨單已結案，但新增問題單失敗                 |
+-----------+------------------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Exchange/QueryStatus
------------------------

查詢換貨狀態

### Request parameters

+------------+-----------------+-------------+
| Parameter  | Value           | Description |
+============+=================+=============+
| ExchangeId | string(Require) | 換貨單序號  |
+------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/QueryStatus&ExchangeId=2121212&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/QueryStatus&ExchangeId=2121212&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+---------------------+----------------+
| Field               | Description    |
+=====================+================+
| TransactionId       | 交易序號       |
+---------------------+----------------+
| OrderId             | 訂單編號       |
+---------------------+----------------+
| ExchangeId          | 換貨單序號     |
+---------------------+----------------+
| ExchangeCreateDate  | 換貨單建立日期 |
+---------------------+----------------+
| ExchangeConfirmDate | 換貨單確認日期 |
+---------------------+----------------+
| ExchangeCloseDate   | 換貨單結案日期 |
+---------------------+----------------+
| ExchangeCloseReason | 換貨單結案原因 |
+---------------------+----------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
      "@Id": 123456,
      "Order": [
        {
          "@Id": "YM1234577",
          "Exchange": {
            "@Id": "EX123456",
            "ExchangeCloseDate": "2010/11/14",
            "ExchangeConfirmDate": "2010/11/12",
            "ExchangeCreateDate": "2010/11/11",
            "_ExchangeCloseReason": "\u5bc4\u51fa\u65b0\u54c1"
          }
        }
      ]
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?><Response Status="ok">
      <Transaction Id="123456">
            <Order Id="YM1234577">
                  <Exchange Id="EX123456">
                        <ExchangeCreateDate>2010/11/11</ExchangeCreateDate>
                        <ExchangeConfirmDate>2010/11/12</ExchangeConfirmDate>
                        <ExchangeCloseDate>2010/11/14</ExchangeCloseDate>
                        <ExchangeCloseReason><![CDATA[寄出新品]]></ExchangeCloseReason>
                  </Exchange>
            </Order>
      </Transaction>
</Response>
```

### Errors

---

/v1/Exchange/GetCloseReasonList
-------------------------------

取得目前設定使用的換貨結案原因代碼對應表,於執行換貨結案時使用

### Response fields

+------------+----------------------------+
| Field      | Description                |
+============+============================+
| ReasonCode | 換貨結案原因代碼           |
|            |                            |
|            | * 1:寄出新品               |
|            | * 3:線上解決問題           |
|            | * 5:換貨轉退貨(派車取貨)   |
|            | * 6:換貨轉退貨(不派車取貨) |
+------------+----------------------------+
| Reason     | 換貨結案原因               |
+------------+----------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Exchange/GetCloseReasonList&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Exchange/GetCloseReasonList&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "ExchangeReasonList": {
      "ExchangeReason": [
        {
          "@Code": "1",
          "_Reason": "\u5bc4\u51fa\u65b0\u54c1"
        },
        {
          "@Code": "3",
          "_Reason": "\u7dda\u4e0a\u89e3\u6c7a\u554f\u984c"
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
      <ExchangeReasonList>
            <ExchangeReason Code="1">
                  <Reason>
                        <![CDATA[寄出新品]]>
                  </Reason>
            </ExchangeReason>
            <ExchangeReason Code="3">
                  <Reason>
                        <![CDATA[線上解決問題]]>
                  </Reason>
            </ExchangeReason>
      </ExchangeReasonList>
</Response>
```

### Errors

