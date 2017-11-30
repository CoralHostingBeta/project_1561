/v1/ReturnAbnormality/Query
---------------------------

查詢退貨異常單

### Request parameters

+-------------------------+-----------------+---------------------------------------------------+
| Parameter               | Value           | Description                                       |
+=========================+=================+===================================================+
| ReturnAbnormalityStatus | string(Require) | 退貨異常狀態                                      |
|                         |                 |                                                   |
|                         |                 | * NonClose：未結案                                |
|                         |                 | * All：全部                                       |
+-------------------------+-----------------+---------------------------------------------------+
| DateType                | string(Require) | 日期條件                                          |
|                         |                 |                                                   |
|                         |                 | * ReturnCreateDate：退貨單建立日期                |
|                         |                 | * ReturnAbnormalityCreateDate：退貨異常單建立日期 |
+-------------------------+-----------------+---------------------------------------------------+
| StartDate               | date(Require)   | 起始日期                                          |
|                         |                 |                                                   |
|                         |                 | (yyyy/mm/dd)                                      |
+-------------------------+-----------------+---------------------------------------------------+
| EndDate                 | date(Require)   | 迄止日期                                          |
|                         |                 |                                                   |
|                         |                 | (yyyy/mm/dd)                                      |
|                         |                 |                                                   |
|                         |                 | EndDate-StartDate要小於等於30天                   |
+-------------------------+-----------------+---------------------------------------------------+
| Position                | int(Require)    | 由第幾筆開始拿資料                                |
+-------------------------+-----------------+---------------------------------------------------+
| Count                   | int(Require)    | 資料筆數                                          |
|                         |                 |                                                   |
|                         |                 | Count=1~100                                       |
+-------------------------+-----------------+---------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/ReturnAbnormality/Query?ReturnAbnormalityStatus=All&DateType=ReturnCreateDate&StartDate=2010/01/01&EndDate=2010/01/02&Position=1&Count=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/ReturnAbnormality/Query?ReturnAbnormalityStatus=All&DateType=ReturnCreateDate&StartDate=2010/01/01&EndDate=2010/01/02&Position=1&Count=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-------------------------+---------------------------------------------------+
| Field                   | Description                                       |
+=========================+===================================================+
| OrderList               | 包含符合查詢條件的Order List，屬性：              |
|                         |                                                   |
|                         | * Count：資料筆數                                 |
+-------------------------+---------------------------------------------------+
| TotalCount              | 符合查詢條件的總資料筆數                          |
+-------------------------+---------------------------------------------------+
| Order                   | 包含一筆訂單的資料，屬性：                        |
|                         |                                                   |
|                         | * Id：訂單編號                                    |
+-------------------------+---------------------------------------------------+
| ReturnList              | 包含一筆訂單的ReturnList資料，屬性：              |
|                         |                                                   |
|                         | * Count：資料筆數                                 |
+-------------------------+---------------------------------------------------+
| Return                  | 包含一筆退貨單的資料，屬性：                      |
|                         |                                                   |
|                         | * Id：退貨單序號                                  |
+-------------------------+---------------------------------------------------+
| ReturnStatus            | 退貨單狀態                                        |
|                         |                                                   |
|                         | * NonClose：未結案                                |
|                         | * Close：結案                                     |
+-------------------------+---------------------------------------------------+
| ReturnAbnormalityList   | 包含一筆退貨單的ReturnAbnormalityList資料，屬性： |
|                         |                                                   |
|                         | * Count：資料筆數                                 |
+-------------------------+---------------------------------------------------+
| ReturnAbnormality       | 包含一筆退貨異常單的資料，屬性：                  |
|                         |                                                   |
|                         | * Id：退貨異常單序號                              |
+-------------------------+---------------------------------------------------+
| ReturnAbnormalityStatus | 退貨異常單狀態                                    |
|                         |                                                   |
|                         | * NonClose：未結案                                |
|                         | * Close：結案                                     |
+-------------------------+---------------------------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "OrderList":
        {
            "@Count":2,
            "@TotalCount":10,
            "Order":
            {
                "@Id":"YM1234567890123",
                "ReturnList":
                {
                    "@Count":"1",
                    "Return":
                    [
                        {
                            "@Id":"123456",
                            "ReturnStatus":"NonClose",
                            "ReturnAbnormalityList":
                            {
                                "@Count":"1",
                                "ReturnAbnormality":
                                [
                                    {
                                        "@Id":"654321",
                                        "ReturnAbnormalityStatus":"NonClose"
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
    <OrderList Count="2" TotalCount="10">
        <Order Id="YM1234567890123">
            <ReturnList Count="1">
                <Return Id="123456">
                    <ReturnStatus>NonClose</ReturnStatus>
                    <ReturnAbnormalityList Count="1">
                        <ReturnAbnormality Id="654321">
                            <ReturnAbnormalityStatus>NonClose</ReturnAbnormalityStatus>
                        </ReturnAbnormality>
                    </ReturnAbnormalityList>
                </Return>
            </ReturnList>
        </Order>
    </OrderList>
</Response>
```

### Errors

---

/v1/ReturnAbnormality/Add
-------------------------

新增退貨異常單

### Request parameters

+-----------------------+-----------------+------------------+
| Parameter             | Value           | Description      |
+=======================+=================+==================+
| ReturnId              | string(Require) | 退貨單序號       |
+-----------------------+-----------------+------------------+
| ProductAbnormalReason | int(Require)    | 商品異常原因     |
+-----------------------+-----------------+------------------+
| ProductAbnormalRemark | string(Option)  | 商品異常備註說明 |
+-----------------------+-----------------+------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/ReturnAbnormality/Add?ReturnId=123456&ProductAbnormalReason=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/ReturnAbnormality/Add?ReturnId=123456&ProductAbnormalReason=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------------------+--------------------+
| Field                       | Description        |
+=============================+====================+
| ReturnAbnormalityId         | 退貨異常單序號     |
+-----------------------------+--------------------+
| ReturnAbnormalityCreateDate | 退貨異常單建立日期 |
+-----------------------------+--------------------+
| ErrorCode                   | 錯誤代碼           |
+-----------------------------+--------------------+
| ErrorMessage                | 錯誤訊息           |
+-----------------------------+--------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "ReturnAbnormality":
        {
            "@Id":"123456",
            "ReturnAbnormalityCreateDate":"2011/11/12"
        }
    }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
    <ReturnAbnormality Id="123456">
        <ReturnAbnormalityCreateDate>2011/11/12</ReturnAbnormalityCreateDate>
    </ReturnAbnormality>
</Response>
```

### Errors

+-----------+--------------------+
| ErrorCode | ErrorMessage       |
+===========+====================+
| 2601      | 退貨單已結案       |
+-----------+--------------------+
| 2602      | 退貨單已取消       |
+-----------+--------------------+
| 2603      | 退貨異常單未結案   |
+-----------+--------------------+
| 2604      | 商品異常原因不存在 |
+-----------+--------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/ReturnAbnormality/Close
---------------------------

執行退貨異常結案

### Request parameters

+------------------------------+-----------------+------------------+
| Parameter                    | Value           | Description      |
+==============================+=================+==================+
| ReturnAbnormalityId          | string(Require) | 退貨異常單序號   |
+------------------------------+-----------------+------------------+
| ReturnAbnormalityCloseRemark | string(Option)  | 退貨異常結案備註 |
+------------------------------+-----------------+------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/ReturnAbnormality/Close?ReturnAbnormalityId=123456&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/ReturnAbnormality/Close?ReturnAbnormalityId=123456&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+---------------------+----------------+
| Field               | Description    |
+=====================+================+
| ReturnAbnormalityId | 退貨異常單序號 |
+---------------------+----------------+
| ErrorCode           | 錯誤代碼       |
+---------------------+----------------+
| ErrorMessage        | 錯誤訊息       |
+---------------------+----------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "ReturnAbnormality":
        {
            "@Id":"123456"
        }
    }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
    <ReturnAbnormality Id="123456"></ReturnAbnormality>
</Response>
```

### Errors

+-----------+--------------------+
| ErrorCode | ErrorMessage       |
+===========+====================+
| 2621      | 此退貨異常單已結案 |
+-----------+--------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/ReturnAbnormality/GetProduct&shy;AbnormalReasonList
-------------------------------------------------------

取得目前設定使用的商品異常原因代碼對應表，於執行新增退貨異常單時使用

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/ReturnAbnormality/GetProductAbnormalReasonList?Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/ReturnAbnormality/GetProductAbnormalReasonList?Format=xml
```

### Response fields

+------------+----------------------------+
| Field      | Description                |
+============+============================+
| ReasonCode | 退貨異常的商品異常原因代碼 |
|            |                            |
|            | * 1：缺配件                |
|            | * 2：商品有問題            |
+------------+----------------------------+
| Reason     | 退貨異常的商品異常原因     |
+------------+----------------------------+

### Sample response

#### JSON sample

```
{
    "Response":
    {
        "@Status":"ok",
        "ProductAbnormalReasonList":
        {
            "ProductAbnormalReason":
            [
                {
                   "@Code":"1",
                   "_Reason":"\u7f3a\u914d\u4ef6"
                },
                {
                   "@Code":"2",
                   "_Reason":"\u5546\u54c1\u6709\u554f\u984c"
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
    <ProductAbnormalReasonList>
        <ProductAbnormalReason Code="1">
            <Reason><![CDATA[缺配件]]></Reason>
        </ProductAbnormalReason>
        <ProductAbnormalReason Code="2">
                <Reason><![CDATA[商品有問題]]></Reason>
        </ProductAbnormalReason>
    </ProductAbnormalReasonList>
</Response>
```

### Errors

