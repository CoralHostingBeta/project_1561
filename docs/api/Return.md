/v1/Return/Query
----------------

退貨查詢,可依據不同的條件查詢退貨單列表

### Request parameters

+--------------+---------------------+----------------------------------+
| Parameter    | Value               | Description                      |
+==============+=====================+==================================+
| ReturnStatus | string (20/Require) | 退貨單狀態                       |
|              |                     |                                  |
|              |                     | * All：全部                      |
|              |                     | * NonClose：未結案               |
|              |                     | * Close：已結案                  |
|              |                     | * Cancel：取消                   |
+--------------+---------------------+----------------------------------+
| DateType     | string (20/Require) | 日期條件                         |
|              |                     |                                  |
|              |                     | * ReturnCreateDate：退貨單建立日 |
|              |                     | * ReturnCloseDate：退貨結案日    |
+--------------+---------------------+----------------------------------+
| StartDate    | date(Require)       | 起始日期                         |
|              |                     |                                  |
|              |                     | (yyyy/mm/dd)                     |
+--------------+---------------------+----------------------------------+
| EndDate      | date(Require)       | 迄止日期                         |
|              |                     |                                  |
|              |                     | (yyyy/mm/dd)                     |
|              |                     |                                  |
|              |                     | EndDate-StartDate 要小於等於7天  |
+--------------+---------------------+----------------------------------+
| Position     | int(Require)        | 由第幾筆開始拿資料               |
+--------------+---------------------+----------------------------------+
| Count        | int(Require)        | 資料筆數                         |
|              |                     |                                  |
|              |                     | Count=1~100                      |
+--------------+---------------------+----------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/Query?ReturnStatus=Close&DateType=ReturnCreateDate&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/Query?ReturnStatus=Close&DateType=ReturnCreateDate&Format=xml
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
| OrderId         | 訂單編號                                   |
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
              "@Id": "YM1234567"
            },
            {
              "@Id": "YM1234568"
            },
            {
              "@Id": "YM1234569"
            }
          ]
        },
        {
          "@Id": "12346",
          "Order": [
            {
              "@Id": "YM1234511"
            },
            {
              "@Id": "YM1234512"
            },
            {
              "@Id": "YM1234513"
            }
          ]
        },
        {
          "@Id": "123488",
          "Order": [
            {
              "@Id": "YM1234599"
            },
            {
              "@Id": "YM1234566"
            },
            {
              "@Id": "YM1234533"
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
      <Order Id="YM1234567"></Order>
      <Order Id="YM1234568"></Order>
      <Order Id="YM1234569"></Order>
    </Transaction>
    <Transaction Id="12346">
      <Order Id="YM1234511"></Order>
      <Order Id="YM1234512"></Order>
      <Order Id="YM1234513"></Order>
    </Transaction>
    <Transaction Id="123488">
      <Order Id="YM1234599"></Order>
      <Order Id="YM1234566"></Order>
      <Order Id="YM1234533"></Order>
    </Transaction>
  </TransactionList>
</Response>
```

### Errors

---

/v1/Return/Get
--------------

取得退貨明細資料

### Request parameters

+---------------+-----------------+-------------+
| Parameter     | Value           | Description |
+===============+=================+=============+
| TransactionId | string(Require) | 交易序號    |
+---------------+-----------------+-------------+
| OrderId       | string(Require) | 訂單編號    |
+---------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/Get?TransactionId=212346&OrderId=12144&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/Get?TransactionId=212346&OrderId=12144&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------------------+---------------------------------------+
| Field                       | Description                           |
+=============================+=======================================+
| TransactionId               | 交易序號                              |
+-----------------------------+---------------------------------------+
| OrderId                     | 訂單編號                              |
+-----------------------------+---------------------------------------+
| ReturnList                  | 包含此訂單的退貨單 List，屬性：       |
|                             |                                       |
|                             | * Count：資料筆數                     |
+-----------------------------+---------------------------------------+
| Return                      | 包含一筆退貨單的資料，屬性：          |
|                             |                                       |
|                             | * Id：退貨單序號                      |
+-----------------------------+---------------------------------------+
| ReturnCreateDate            | 退貨單建立日                          |
+-----------------------------+---------------------------------------+
| ReturnReason                | 退貨原因                              |
+-----------------------------+---------------------------------------+
| ReturnReasonRemark          | 退貨原因備註                          |
+-----------------------------+---------------------------------------+
| ReturnPickupName            | 退貨取件姓名                          |
+-----------------------------+---------------------------------------+
| ReturnPickupMobile          | 退貨取件手機                          |
+-----------------------------+---------------------------------------+
| ReturnPickupPhone           | 退貨取件電話                          |
+-----------------------------+---------------------------------------+
| ReturnPickupZipcode         | 退貨取件郵遞區號                      |
+-----------------------------+---------------------------------------+
| ReturnPickupAddress         | 退貨取件地址                          |
+-----------------------------+---------------------------------------+
| ReturnPrice                 | 退貨金額                              |
+-----------------------------+---------------------------------------+
| ReturnStatus                | 退貨狀態                              |
|                             |                                       |
|                             | * NonClose：未結案                    |
|                             | * Close：已結案                       |
|                             | * Cancel：取消                        |
+-----------------------------+---------------------------------------+
| ReturnCloseDate             | 退貨結案日                            |
+-----------------------------+---------------------------------------+
| ReturnDebitDate             | 退貨扣帳日                            |
+-----------------------------+---------------------------------------+
| ProductId                   | 商品編號                              |
+-----------------------------+---------------------------------------+
| CustomizedProductId         | 自訂貨號                              |
+-----------------------------+---------------------------------------+
| ProductName                 | 商品名稱                              |
+-----------------------------+---------------------------------------+
| Spec                        | 商品規格                              |
+-----------------------------+---------------------------------------+
| ReturnAbnormalityList       | 包含此退貨單的退貨異常單 List，屬性： |
|                             |                                       |
|                             | * Count：資料筆數                     |
+-----------------------------+---------------------------------------+
| ReturnAbnormality           | 包含一筆退貨異常單的資料，屬性：      |
|                             |                                       |
|                             | * Id：退貨異常單序號                  |
+-----------------------------+---------------------------------------+
| ReturnAbnormalityCreateDate | 退貨異常單建立日期                    |
+-----------------------------+---------------------------------------+
| ReturnAbnormalityReason     | 退貨異常原因                          |
+-----------------------------+---------------------------------------+
| ReturnAbnormalityRemark     | 退貨異常原因備註                      |
+-----------------------------+---------------------------------------+
| ReturnAbnormalityStatus     | 退貨異常狀態                          |
+-----------------------------+---------------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "Transaction":
        {
            "@Id":123456,
            "Order":
            {
                "@Id":"YM1234577",
                "ReturnList":
                {
                    "@Count":2,
                    "Return":
                    [
                        {
                            "@Id":"123456",
                            "ReturnCreateDate":"2010/11/15",
                            "_ReturnReason":"\u4e0d\u559c\u6b61",
                            "_ReturnReasonRemark":"xx",
                            "_ReturnPickupName":"\u9673\u7f8e\u7f8e",
                            "_ReturnPickupMobile":"0922222222",
                            "_ReturnPickupPhone":"0911111111",
                            "_ReturnPickupAddress":"\u53f0\u5317\u5e02\u58eb\u6797\u5340\u6587\u5316\u8def1\u865f",
                            "ReturnPrice":100,
                            "ReturnStatus":"Close",
                            "ReturnCloseDate":"2010/12/1",
                            "ReturnDebitDate":"2010/12/15",
                            "ProductId":"p1234212",
                            "CustomizeId":"A12345",
                            "ProductName":"\u7537\u7528\u5167\u8863",
                            "Spec":"\u7d05\u8272",
                            "ReturnAbnormalityList":
                            {
                                "@Count":1,
                                "ReturnAbnormality":
                                [
                                    {
                                        "@Id":"123456",
                                        "ReturnAbnormalityCreateDate":"2010/12/15",
                                        "ReturnAbnormalityReason":2,
                                        "_ReturnAbnormalityRemark":"\u5546\u54c1\u6709\u554f\u984c",
                                        "ReturnAbnormalityStatus":"NonClose"
                                    }
                                ]
                            }
                        },
                        {
                            "@Id":"123888",
                            "ReturnCreateDate":"2010/11/15",
                            "_ReturnReason":"\u5927\u5ea7\u4e0d\u559c\u6b61",
                            "_ReturnReasonRemark":"xx",
                            "_ReturnPickupName":"\u9673\u7f8e\u7f8e",
                            "_ReturnPickupMobile":"0922222222",
                            "_ReturnPickupPhone":"0911111111",
                            "_ReturnPickupAddress":"\u53f0\u5317\u5e02\u58eb\u6797\u5340\u6587\u5316\u8def1\u865f",
                            "ReturnPrice":200,
                            "ReturnStatus":"Close",
                            "ReturnCloseDate":"2010/12/1",
                            "ReturnDebitDate":"2010/12/15",
                            "ProductId":"p1234233",
                            "CustomizeId":"A123XX",
                            "ProductName":"\u5973\u7528\u5167\u8863",
                            "Spec":"\u8089\u8272",
                            "ReturnAbnormalityList":
                            {
                                "@Count":1,
                                "ReturnAbnormality":
                                [
                                    {
                                        "@Id":"123457",
                                        "ReturnAbnormalityCreateDate":"2010/12/15",
                                        "ReturnAbnormalityReason":1,
                                        "_ReturnAbnormalityRemark":"",
                                        "ReturnAbnormalityStatus":"Close"
                                    }
                                ]
                            }
                        }
                    ]
                }
            }
        }
    }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
    <Transaction Id="123456">
        <Order Id="YM1234577">
            <ReturnList Count="2">
                <Return Id="123456">
                    <ReturnCreateDate>2010/11/15</ReturnCreateDate>
                    <ReturnReason><![CDATA[不喜歡]]></ReturnReason>
                    <ReturnReasonRemark><![CDATA[xx]]></ReturnReasonRemark>
                    <ReturnPickupName><![CDATA[陳美美]]></ReturnPickupName>
                    <ReturnPickupMobile><![CDATA[0922222222]]></ReturnPickupMobile>
                    <ReturnPickupPhone><![CDATA[0911111111]]></ReturnPickupPhone>
                    <ReturnPickupAddress><![CDATA[台北市士林區文化路1號]]></ReturnPickupAddress>
                    <ReturnPrice>100</ReturnPrice>
                    <ReturnStatus>Close</ReturnStatus>
                    <ReturnCloseDate>2010/12/1</ReturnCloseDate>
                    <ReturnDebitDate>2010/12/15</ReturnDebitDate>
                    <ProductId>p1234212</ProductId>
                    <CustomizeId>A12345</CustomizeId>
                    <ProductName>男用內衣</ProductName>
                    <Spec>紅色</Spec>
                    <ReturnAbnormalityList Count="1">
                        <ReturnAbnormality Id="123456">
                            <ReturnAbnormalityCreateDate>2010/12/15</ReturnAbnormalityCreateDate>
                            <ReturnAbnormalityReason>2</ReturnAbnormalityReason>
                            <ReturnAbnormalityRemark><![CDATA[商品有問題]]></ReturnAbnormalityRemark>
                            <ReturnAbnormalityStatus>NonClose</ReturnAbnormalityStatus>
                         </ReturnAbnormality>
                    </ReturnAbnormalityList>
                </Return>
                <Return Id="123888">
                    <ReturnCreateDate>2010/11/15</ReturnCreateDate>
                    <ReturnReason><![CDATA[大座不喜歡]]></ReturnReason>
                    <ReturnReasonRemark><![CDATA[xx]]></ReturnReasonRemark>
                    <ReturnPickupName><![CDATA[陳美美]]></ReturnPickupName>
                    <ReturnPickupMobile><![CDATA[0922222222]]></ReturnPickupMobile>
                    <ReturnPickupPhone><![CDATA[0911111111]]></ReturnPickupPhone>
                    <ReturnPickupAddress><![CDATA[台北市士林區文化路1號]]></ReturnPickupAddress>
                    <ReturnPrice>200</ReturnPrice>
                    <ReturnStatus>Close</ReturnStatus>
                    <ReturnCloseDate>2010/12/1</ReturnCloseDate>
                    <ReturnDebitDate>2010/12/15</ReturnDebitDate>
                    <ProductId>p1234233</ProductId>
                    <CustomizeId>A123XX</CustomizeId>
                    <ProductName>女用內衣</ProductName>
                    <Spec>肉色</Spec>
                    <ReturnAbnormalityList Count="1">
                        <ReturnAbnormality Id="123457">
                            <ReturnAbnormalityCreateDate>2010/12/15</ReturnAbnormalityCreateDate>
                            <ReturnAbnormalityReason>1</ReturnAbnormalityReason>
                            <ReturnAbnormalityRemark><![CDATA[]]></ReturnAbnormalityRemark>
                            <ReturnAbnormalityStatus>Close</ReturnAbnormalityStatus>
                        </ReturnAbnormality>
                    </ReturnAbnormalityList>
                </Return>
            </ReturnList>
        </Order>
   </Transaction>
</Response>
```

### Errors

---

/v1/Return/Add
--------------

新增退貨單

### Request parameters

+----------------------------+-----------------+-------------------------------------+
| Parameter                  | Value           | Description                         |
+============================+=================+=====================================+
| TransactionId              | string(Require) | 交易序號                            |
+----------------------------+-----------------+-------------------------------------+
| OrderId                    | string(Require) | 訂單編號                            |
+----------------------------+-----------------+-------------------------------------+
| ReturnReason               | int(Require)    | 退貨原因                            |
|                            |                 |                                     |
|                            |                 | 請參閱/Return/GetReasonList填入代碼 |
+----------------------------+-----------------+-------------------------------------+
| ReturnReasonDesc           | string(Option)  | 退貨原因描述                        |
+----------------------------+-----------------+-------------------------------------+
| ReturnPickupName           | string(Option)  | 取貨客戶姓名                        |
+----------------------------+-----------------+-------------------------------------+
| ReturnPickupZipcode        | string(Require) | 取貨地址的郵遞區號                  |
+----------------------------+-----------------+-------------------------------------+
| ReturnPickupAddress        | string(Require) | 取貨地址(不含縣市/郵遞區號)         |
+----------------------------+-----------------+-------------------------------------+
| ReturnPickupMobile         | string(Option)  | 取貨聯連絡電話手機                  |
+----------------------------+-----------------+-------------------------------------+
| ReturnPickupSecondaryPhone | string(Option)  | 取貨次要聯絡電話                    |
+----------------------------+-----------------+-------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/Add?TransactionId=123456&OrderId=YM1234567890123&ReturnReason=1&ReturnPickupZipcode=100&ReturnPickupAddress=市民大道100號&Count=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/Add?TransactionId=123456&OrderId=YM1234567890123&ReturnReason=1&ReturnPickupZipcode=100&ReturnPickupAddress=市民大道100號&Count=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+------------------+-------------------------------+
| Field            | Description                   |
+==================+===============================+
| ReturnList       | 包含新增的退貨單 List，屬性： |
|                  |                               |
|                  | * Count：資料筆數             |
+------------------+-------------------------------+
| Return           | 包含一筆退貨單的資料，屬性：  |
|                  |                               |
|                  | * Id：退貨單序號              |
+------------------+-------------------------------+
| ReturnCreateDate | 退貨單建立日                  |
+------------------+-------------------------------+
| ErrorCode        | 錯誤代碼                      |
+------------------+-------------------------------+
| ErrorMessage     | 錯誤訊息                      |
+------------------+-------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "ReturnList":
        {
            "@Count":2,
            "Return":
            [
                {
                    "@Id":"123456",
                    "ReturnCreateDate":"2011/11/12"
                },
                {
                    "@Id":"123457",
                    "ReturnCreateDate":"2011/11/12"
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
    <ReturnList Count="2">
        <Return Id="123456">
            <ReturnCreateDate>2011/11/12</ReturnCreateDate>
        </Return>
        <Return Id="123457">
            <ReturnCreateDate>2011/11/12</ReturnCreateDate>
        </Return>
    </ReturnList>
</Response>
```

### Errors

+-----------+-------------------------------------+
| ErrorCode | ErrorMessage                        |
+===========+=====================================+
| 2401      | 此訂單未出貨，無法退貨              |
+-----------+-------------------------------------+
| 2402      | 此訂單已產生退貨單/換貨單，無法新增 |
+-----------+-------------------------------------+
| 2403      | 新增退貨單成功，但寄發通知信失敗    |
+-----------+-------------------------------------+
| 2404      | 退貨原因不存在                      |
+-----------+-------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Return/Confirm
------------------

執行退貨確認

### Request parameters

+---------------+-----------------+-------------+
| Parameter     | Value           | Description |
+===============+=================+=============+
| TransactionId | string(Require) | 交易序號    |
+---------------+-----------------+-------------+
| OrderId       | string(Require) | 訂單編號    |
+---------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/Confirm?TransactionId=212346&OrderId=12144&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/Confirm?TransactionId=212346&OrderId=12144&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------+-------------+
| Field           | Description |
+=================+=============+
| ReturnCloseDate | 退貨結案日  |
+-----------------+-------------+
| ErrorCode       | 錯誤代碼    |
+-----------------+-------------+
| ErrorMessage    | 錯誤訊息    |
+-----------------+-------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
      "@Id": "123456",
      "Order": {
        "@Id": "YM1234567",
        "ReturnCloseDate": "2010/11/12"
      }
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Transaction Id="123456">
            <Order Id="YM1234567">
                  <ReturnCloseDate>2010/11/12</ReturnCloseDate>
            </Order>
      </Transaction>
</Response>
```

### Errors

+-----------+------------------+
| ErrorCode | ErrorMessage     |
+===========+==================+
| 2501      | 退貨單已取消     |
+-----------+------------------+
| 2502      | 有退貨異常未結案 |
+-----------+------------------+
| 2503      | 退貨單已結案     |
+-----------+------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Return/Cancel
-----------------

執行取消退貨單

### Request parameters

+---------------+-------------------+-------------+
| Parameter     | Value             | Description |
+===============+===================+=============+
| TransactionId | string(Require)   | 交易序號    |
+---------------+-------------------+-------------+
| OrderId       | string(Require)   | 訂單編號    |
+---------------+-------------------+-------------+
| CancelReason  | string(?/Require) | 取消原因    |
+---------------+-------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/Cancel?TransactionId=212346&OrderId=12144&CancelReason=wrong_color&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/Cancel?TransactionId=212346&OrderId=12144&CancelReason=wrong_color&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+------------------+-------------+
| Field            | Description |
+==================+=============+
| ReturnCancelDate | 退貨取消日  |
+------------------+-------------+
| ErrorCode        | 錯誤代碼    |
+------------------+-------------+
| ErrorMessage     | 錯誤訊息    |
+------------------+-------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
      "@Id": "123456",
      "Order": {
        "@Id": "YM1234567",
        "ReturnCancelDate": "2010/11/12"
      }
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Transaction Id="123456">
            <Order Id="YM1234567">
                  <ReturnCancelDate>2010/11/12</ReturnCancelDate>
            </Order>
      </Transaction>
</Response>
```

### Errors

+-----------+------------------------------------+
| ErrorCode | ErrorMessage                       |
+===========+====================================+
| 2521      | 退貨單已取消                       |
+-----------+------------------------------------+
| 2522      | 無法取消退貨單：退貨單已結案       |
+-----------+------------------------------------+
| 2523      | 無法取消退貨單：尚有退貨異常未結案 |
+-----------+------------------------------------+
| 2524      | 無法取消退貨單：已產生貨運單       |
+-----------+------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Return/GetReasonList
------------------------

取得目前設定使用的退貨原因代碼對應表，於執行新增退貨單時使用

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Return/GetReasonList?Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Return/GetReasonList?Format=xml
```

### Response fields

+------------+--------------------+
| Field      | Description        |
+============+====================+
| ReturnCode | 退貨原因代碼       |
|            |                    |
|            | * 1：新品瑕疵故障  |
|            | * 2：商品不如預期  |
|            | * 3：商品規格不符  |
|            | * 5：未如期交貨    |
|            | * 7：價格比別家貴  |
|            | * 14：重複購買了   |
|            | * 25：我要改買別款 |
|            | * 90：其他         |
+------------+--------------------+
| Reason     | 退貨原因           |
+------------+--------------------+

### Sample response

#### JSON sample

```
{"Response":
  {
    "@Status":"ok",
    "ReturnReasonList":
    {
        "ReturnReason":
        [
            {
                "@Code":"1",
                "_Reason":"\u65b0\u54c1\u7455\u75b5\u6545\u969c"
            },{
                "@Code":"2",
                "_Reason":"\u5546\u54c1\u4e0d\u5982\u9810\u671f"
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
  <ReturnReasonList>
    <ReturnReason Code="1">
      <Reason><![CDATA[新品瑕疵故障]]></Reason>
    </ReturnReason>
    <ReturnReason Code="2">
      <Reason><![CDATA[商品不如預期]]></Reason>
    </ReturnReason>
  </ReturnReasonList>
</Response>
```

### Errors

