/v1/Cancel/Query
----------------

取消訂單查詢,可依據不同的條件查詢取消訂單列表

### Request parameters

+--------------+--------------------+--------------------------------+
| Parameter    | Value              | Description                    |
+==============+====================+================================+
| CancelReason | string(Require)    | 取消原因                       |
|              |                    |                                |
|              |                    | * All:全部                     |
|              |                    | * CancelByBuyer:買家取消       |
|              |                    | * Overdue:逾期未出貨           |
|              |                    | * CancelBySeller:店家取消      |
|              |                    | * Others:其他                  |
+--------------+--------------------+--------------------------------+
| DateType     | string(20/Require) | 日期條件                       |
|              |                    |                                |
|              |                    | * OrderDate:訂購日             |
|              |                    | * OrderCloseDate:訂單結案日    |
+--------------+--------------------+--------------------------------+
| StartDate    | date(Require)      | 起始日期                       |
|              |                    |                                |
|              |                    | (yyyy/mm/dd)                   |
+--------------+--------------------+--------------------------------+
| EndDate      | date(Require)      | 迄止日期                       |
|              |                    |                                |
|              |                    | (yyyy/mm/dd)                   |
|              |                    |                                |
|              |                    | EndDate-StartDate要小於等於7天 |
+--------------+--------------------+--------------------------------+
| Position     | int(Require)       | 由第幾筆開始拿資料             |
+--------------+--------------------+--------------------------------+
| Count        | int(Require)       | 資料筆數                       |
|              |                    |                                |
|              |                    | Count=1~100                    |
+--------------+--------------------+--------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Cancel/Query?CancelReason=All&DateType=OrderDate&StartDate=2011/01/01&EndDate=2011/01/02&Position=1&Count=1
                                                                            OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Cancel/Query?CancelReason=All&DateType=OrderDate&StartDate=2011/01/01&EndDate=2011/01/02&Position=1&Count=1
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
| OrderStatus     | 訂單狀態                                   |
|                 |                                            |
|                 | * NEW:未結案                               |
|                 | * CANCEL:取消                              |
|                 | * SHIPPED:完成出貨                         |
+-----------------+--------------------------------------------+
| OrderStatusDesc | 訂單狀態描述                               |
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
              "OrderStatus": "NEW",
              "OrderStatusDesc": "未結案"
            },
            {
              "@Id": "YM1234568",
              "OrderStatus": "SHIPPED",
              "OrderStatusDesc": "完成出貨"
            },
            {
              "@Id": "YM1234569",
              "OrderStatus": "CANCEL",
              "OrderStatusDesc": "取消-缺貨"
            },
            {
              "@Id": "YM1234560",
              "OrderStatus": "CANCEL",
              "OrderStatusDesc": "取消-門市刷退"
            }
          ]
        },
        {
          "@Id": "12346",
          "Order": [
            {
              "@Id": "YM1234511",
              "OrderStatus": "NEW",
              "OrderStatusDesc": "未結案"
            },
            {
              "@Id": "YM1234512",
              "OrderStatus": "SHIPPED",
              "OrderStatusDesc": "完成出貨"
            }, 
            {
              "@Id": "YM1234513",
              "OrderStatus": "CANCEL",
              "OrderStatusDesc": "取消-缺貨"
            },
            {
              "@Id": "YM1234514",
              "OrderStatus": "CANCEL",
              "OrderStatusDesc": "取消-門市刷退"
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
                        <OrderStatus>NEW</OrderStatus>
                        <OrderStatusDesc>未結案</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234568">
                        <OrderStatus>SHIPPED</OrderStatus>
                        <OrderStatusDesc>完成出貨</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234569">
                        <OrderStatus>CANCEL</OrderStatus>
                        <OrderStatusDesc>取消-缺貨</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234560">
                        <OrderStatus>CANCEL</OrderStatus>
                        <OrderStatusDesc>取消-門市刷退</OrderStatusDesc>
                  </Order>
            </Transaction>
            <Transaction Id="12346"> 
                 <Order Id="YM1234511">
                        <OrderStatus>NEW</OrderStatus>
                        <OrderStatusDesc>未結案</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234512">
                        <OrderStatus>SHIPPED</OrderStatus>
                        <OrderStatusDesc>完成出貨</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234513">
                        <OrderStatus>CANCEL</OrderStatus>
                        <OrderStatusDesc>取消-缺貨</OrderStatusDesc>
                  </Order>
                  <Order Id="YM1234514">
                        <OrderStatus>CANCEL</OrderStatus>
                        <OrderStatusDesc>取消-門市刷退</OrderStatusDesc>
                  </Order>
            </Transaction>
      </TransactionList>
</Response>
```

### Errors

