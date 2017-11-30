/v1/OrderShipping/Confirm&shy;HomeDelivery (Deprecated)
-------------------------------------------------------

!!! caution "Deprecated"

對宅配訂單執行出貨確認

### Request parameters

+----------------------+---------------------+-------------+
| Parameter            | Value               | Description |
+======================+=====================+=============+
| TransactionId        | string (Require)    | 交易序號    |
+----------------------+---------------------+-------------+
| OrderId              | string (Require)    | 訂單編號    |
+----------------------+---------------------+-------------+
| ShippingSupplierCode | int (Optional)      | 物流商代碼  |
+----------------------+---------------------+-------------+
| ShippingNumber       | string (Optional)   | 貨運單號    |
+----------------------+---------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/ConfirmHomeDelivery?TransactionId=21410233&OrderId=2001&Formal=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/ConfirmHomeDelivery?TransactionId=21410233&OrderId=2001&Formal=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+--------------------------+-------------+
| Field                    | Description |
+==========================+=============+
| OrderShippingConfirmDate | 出貨確認日  |
+--------------------------+-------------+
| ErrorCode                | 錯誤代碼    |
+--------------------------+-------------+
| ErrorMessage             | 錯誤訊息    |
+--------------------------+-------------+

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
        "OrderShippingConfirmDate": "2010/11/12"
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
                  <OrderShippingConfirmDate>2010/11/12</OrderShippingConfirmDate>
            </Order>
      </Transaction>
</Response>
```

### Errors

+-----------+------------------------------------+
| ErrorCode | ErrorMessage                       |
+===========+====================================+
| 2101      | 為物流處理費                       |
+-----------+------------------------------------+
| 2102      | 訂單非未出貨狀態                   |
+-----------+------------------------------------+
| 2103      | 非宅配訂單                         |
+-----------+------------------------------------+
| 2104      | 若沒有非未出貨的訂單子單，才能出貨 |
+-----------+------------------------------------+
| 2109      | 無資料或尚未轉單到SCM              |
+-----------+------------------------------------+
| 2110      | 物流商代碼不存在                   |
+-----------+------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v2/OrderShipping/Confirm&shy;HomeDelivery (New)
------------------------------------------------

對宅配訂單執行出貨確認

### Request parameters

+----------------------+------------------+-------------+
| Parameter            | Value            | Description |
+======================+==================+=============+
| TransactionId        | string (Require) | 交易序號    |
+----------------------+------------------+-------------+
| OrderId              | string (Require) | 訂單編號    |
+----------------------+------------------+-------------+
| ShippingSupplierCode | int (Require)    | 物流商代碼  |
+----------------------+------------------+-------------+
| ShippingNumber       | string (Require) | 貨運單號    |
+----------------------+------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v2/OrderShipping/ConfirmHomeDelivery?TransactionId=21410233&OrderId=2001&ShippingSupplierCode=4&ShippingNumber=1234567890&Formal=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v2/OrderShipping/ConfirmHomeDelivery?TransactionId=21410233&OrderId=2001&ShippingSupplierCode=4&ShippingNumber=1234567890&Formal=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+--------------------------+-------------+
| Field                    | Description |
+==========================+=============+
| OrderShippingConfirmDate | 出貨確認日  |
+--------------------------+-------------+
| ErrorCode                | 錯誤代碼    |
+--------------------------+-------------+
| ErrorMessage             | 錯誤訊息    |
+--------------------------+-------------+

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
        "OrderShippingConfirmDate": "2010/11/12"
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
                  <OrderShippingConfirmDate>2010/11/12</OrderShippingConfirmDate>
            </Order>
      </Transaction>
</Response>
```

### Errors

+-----------+------------------------------------+
| ErrorCode | ErrorMessage                       |
+===========+====================================+
| 2101      | 為物流處理費                       |
+-----------+------------------------------------+
| 2102      | 訂單非未出貨狀態                   |
+-----------+------------------------------------+
| 2103      | 非宅配訂單                         |
+-----------+------------------------------------+
| 2104      | 若沒有非未出貨的訂單子單，才能出貨 |
+-----------+------------------------------------+
| 2109      | 無資料或尚未轉單到SCM              |
+-----------+------------------------------------+
| 2110      | 物流商代碼不存在                   |
+-----------+------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/OrderShipping/QueryStore&shy;Delivery&shy;Receipt
------------------------------------------------

查詢超商出貨單

### Request parameters

+-------------------------------+---------------+---------------------------------------------------------------------------+
| Parameter                     | Value         | Description                                                               |
+===============================+===============+===========================================================================+
| StartOrderShippingConfirmDate | Date(Require) | 起始出貨確認日期                                                          |
|                               |               |                                                                           |
|                               |               | (yyyy/mm/dd)                                                              |
+-------------------------------+---------------+---------------------------------------------------------------------------+
| EndOrderShippingConfirmDate   | Date(Require) | 迄止出貨確認日期                                                          |
|                               |               |                                                                           |
|                               |               | (yyyy/mm/dd)                                                              |
|                               |               |                                                                           |
|                               |               | EndOrderShippingConfirmDate - StartOrderShippingConfirmDate 要小於等於3天 |
+-------------------------------+---------------+---------------------------------------------------------------------------+
| Position                      | int(Require)  | 由第幾筆開始拿資料                                                        |
+-------------------------------+---------------+---------------------------------------------------------------------------+
| Count                         | int(Require)  | 資料筆數                                                                  |
|                               |               |                                                                           |
|                               |               | Count=1~100                                                               |
+-------------------------------+---------------+---------------------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/QueryStoreDeliveryReceipt?StartOrderShippingConfirmDate=2010/01/01&EndOrderShippingConfirmDate=2010/01/02&Position=1&Count=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/QueryStoreDeliveryReceipt?StartOrderShippingConfirmDate=2010/01/01&EndOrderShippingConfirmDate=2010/01/02&Position=1&Count=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-------------------------------+--------------------------------------------+
| Field                         | Description                                |
+===============================+============================================+
| TransactionList               | 包含符合查詢條件的Transaction List，屬性： |
|                               |                                            |
|                               | * Count：資料筆數                          |
+-------------------------------+--------------------------------------------+
| TotalCount                    | 符合查詢條件的總資料筆數                   |
+-------------------------------+--------------------------------------------+
| Transaction                   | 包含一筆Transaction的資料，屬性：          |
|                               |                                            |
|                               | * Id：交易序號                             |
+-------------------------------+--------------------------------------------+
| StoreType                     | 超商種類                                   |
|                               |                                            |
|                               | * 7-11：7-11(統一超商)                     |
|                               | * Family：全家超商                         |
|                               | * HiLife：萊爾富超商                       |
|                               | * None：未使用超商                         |
+-------------------------------+--------------------------------------------+
| DeliveryReceiptList           | 包含此筆交易的DeliveryReceipt，屬性：      |
|                               |                                            |
|                               | * Count：資料筆數                          |
+-------------------------------+--------------------------------------------+
| DeliveryReceipt               | 包含一筆DeliveryReceipt的資料，屬性：      |
|                               |                                            |
|                               | * Id：出貨單編號                           |
+-------------------------------+--------------------------------------------+
| DistributionChannelStatus     | 超商通路狀態                               |
|                               |                                            |
|                               | * 0：產生出貨單                            |
|                               | * 1：已轉訂單至超商                        |
|                               | * 2：貨到門市(到店)                        |
|                               | * 3：通路驗收失敗                          |
|                               | * 4：進貨驗收成功                          |
|                               | * 9：未到貨                                |
|                               | * A：顧客取貨                              |
|                               | * B：門市刷退                              |
|                               | * C1：不明件-遺失賠償                      |
|                               | * C2：不明件-異常退貨(代收又驗退)          |
+-------------------------------+--------------------------------------------+
| DistributionChannelStatusDesc | 超商通路狀態描述                           |
+-------------------------------+--------------------------------------------+
| OrderList                     | 包含此筆出貨單的OrderList，屬性：          |
|                               |                                            |
|                               | * Count：資料筆數                          |
+-------------------------------+--------------------------------------------+
| Order                         | 包含一筆Order的資料，屬性：                |
|                               |                                            |
|                               | * Id：訂單編號                             |
+-------------------------------+--------------------------------------------+
| OrderStatue                   | 訂單狀態                                   |
|                               |                                            |
|                               | * NEW：未結案                              |
|                               | * CANCEL：取消                             |
|                               | * SHIPPED：完成出貨                        |
+-------------------------------+--------------------------------------------+
| OrderStatusDesc               | 訂單狀態描述                               |
+-------------------------------+--------------------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "TransactionList":
        {
            "@Count":1,
            "@TotalCount":10,
            "Transaction":
            [
                {
                    "@Id":"1234567",
                    "StoreType":"7-11",
                    "DeliveryReceiptList":
                    [
                        {
                            "@Count":"1",
                            "DeliveryReceipt":
                            [
                                {
                                    "@Id":7654321,
                                    "DistributionChannelStatus":"0",
                                    "_DistributionChannelStatusDesc":"\u7522\u751f\u51fa\u8ca8\u55ae",
                                    "OrderList":
                                    {
                                        "@Count":"2",
                                        "Order":
                                        [
                                            {
                                                "@Id":"YM1008310000077",
                                                "OrderStatus":"NEW",
                                                "_OrderStatusDesc":"\u672a\u7d50\u6848"
                                            },
                                            {
                                                "@Id":"YM1008310000078",
                                                "OrderStatus":"NEW",
                                                "_OrderStatusDesc":"\u672a\u7d50\u6848"
                                            }
                                        ]
                                    }
                                }
                            ]
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
    <TransactionList Count="1" TotalCount="10">
        <Transaction Id="1234567">
            <StoreType>7-11</StoreType>
            <DeliveryReceiptList Count="1">
                <DeliveryReceipt Id="7654321">
                    <DistributionChannelStatus>0</DistributionChannelStatus>
                    <DistributionChannelStatusDesc><![CDATA[產生出貨單]]></DistributionChannelStatusDesc>
                    <OrderList Count="2">
                        <Order Id="YM1008310000077">
                            <OrderStatus>NEW</OrderStatus>
                            <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
                         </Order>
                         <Order Id="YM1008310000078">
                            <OrderStatus>NEW</OrderStatus>
                            <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
                         </Order>
                    </OrderList>
                </DeliveryReceipt>
            </DeliveryReceiptList>
        </Transaction>
    </TransactionList>
</Response>
```

### Errors

---

/v1/OrderShipping/GetStore&shy;DeliveryReceiptDetail
----------------------------------------------------

取得超商出貨單明細資料

### Request parameters

+-------------------+------------------+-------------+
| Parameter         | Value            | Description |
+===================+==================+=============+
| DeliveryReceiptId | string (Require) | 出貨單編號  |
+-------------------+------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/GetStoreDeliveryReceiptDetail?DeliveryReceiptId=123456&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/GetStoreDeliveryReceiptDetail?DeliveryReceiptId=123456&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+----------------------------------+--------------------------------------------------------------+
| Field                            | Description                                                  |
+==================================+==============================================================+
| DeliveryReceiptId                | 出貨單編號                                                   |
+----------------------------------+--------------------------------------------------------------+
| TransactionId                    | 交易序號                                                     |
+----------------------------------+--------------------------------------------------------------+
| StoreType                        | 超商種類                                                     |
|                                  |                                                              |
|                                  | * 7-11：7-11(統一超商)                                       |
|                                  | * Family：全家超商                                           |
|                                  | * HiLife：萊爾富超商                                         |
|                                  | * None：未使用超商                                           |
+----------------------------------+--------------------------------------------------------------+
| SerialNumber                     | For列印超商標籤時使用                                        |
+----------------------------------+--------------------------------------------------------------+
| DeliveryReceiptPrice             | 出貨單金額                                                   |
+----------------------------------+--------------------------------------------------------------+
| DistributionChannelStatus        | 通路狀態                                                     |
|                                  |                                                              |
|                                  | * 0：產生出貨單                                              |
|                                  | * 1：已轉訂單至超商                                          |
|                                  | * 2：貨到門市(到店)                                          |
|                                  | * 3：通路驗收失敗                                            |
|                                  | * 4：進貨驗收成功                                            |
|                                  | * 9：未到貨                                                  |
|                                  | * A：顧客取貨                                                |
|                                  | * B：門市刷退                                                |
|                                  | * C1：不明件-遺失賠償                                        |
|                                  | * C2：不明件-異常退貨(代收又驗退)                            |
+----------------------------------+--------------------------------------------------------------+
| DistributionChannelStatusDesc    | 通路狀態描述                                                 |
+----------------------------------+--------------------------------------------------------------+
| OrderShippingConfirmDate         | 出貨確認日                                                   |
+----------------------------------+--------------------------------------------------------------+
| LastDeliveryDate                 | 最晚送貨日                                                   |
+----------------------------------+--------------------------------------------------------------+
| OrderDelayShippingDate           | 可以延遲出貨日                                               |
+----------------------------------+--------------------------------------------------------------+
| ReceiverName                     | 收件者姓名                                                   |
+----------------------------------+--------------------------------------------------------------+
| TakeDeliveryConvenienceStoreName | 取貨門市名稱                                                 |
+----------------------------------+--------------------------------------------------------------+
| TakeDeliveryConvenienceStoreId   | 取貨門市代碼                                                 |
+----------------------------------+--------------------------------------------------------------+
| Barcode                          | 條碼                                                         |
+----------------------------------+--------------------------------------------------------------+
| DeliveryToConvenienceStoreDate   | 門市進貨日（貨品抵達門市日期）                               |
+----------------------------------+--------------------------------------------------------------+
| ConvenienceStoreReturnDate       | 門市退貨日（門市退回貨品日期）                               |
+----------------------------------+--------------------------------------------------------------+
| ConvenienceStoreOrderId          | 廠商訂單編號                                                 |
+----------------------------------+--------------------------------------------------------------+
| StoreName                        | 商店名稱                                                     |
+----------------------------------+--------------------------------------------------------------+
| CustomerCareInfo                 | 客服資訊                                                     |
+----------------------------------+--------------------------------------------------------------+
| Url                              | 網址                                                         |
+----------------------------------+--------------------------------------------------------------+
| SenderName                       | 寄件人姓名                                                   |
+----------------------------------+--------------------------------------------------------------+
| OrderList                        | 包含此筆出貨單的OrderList，屬性：                            |
|                                  |                                                              |
|                                  | * Count：資料筆數                                            |
+----------------------------------+--------------------------------------------------------------+
| Order                            | 包含一筆Order的資料，屬性：                                  |
|                                  |                                                              |
|                                  | * Id：訂單編號                                               |
+----------------------------------+--------------------------------------------------------------+
| OrderStatus                      | 訂單狀態                                                     |
|                                  |                                                              |
|                                  | * NEW：未結案                                                |
|                                  | * CANCEL：取消                                               |
|                                  | * SHIPPED：完成出貨                                          |
+----------------------------------+--------------------------------------------------------------+
| DeliverType                      | 交寄方式                                                     |
+----------------------------------+--------------------------------------------------------------+
| OrderStatusDesc                  | 訂單狀態描述                                                 |
+----------------------------------+--------------------------------------------------------------+
| LastShippingDate                 | 最晚出貨日                                                   |
+----------------------------------+--------------------------------------------------------------+
| OrderProductList                 | 包含此筆訂單的Order Product List，屬性                       |
|                                  |                                                              |
|                                  | * Count：資料筆數                                            |
+----------------------------------+--------------------------------------------------------------+
| Product                          | 包含一筆訂購的商品資料，屬性：                               |
|                                  |                                                              |
|                                  | * Id：商品編號                                               |
+----------------------------------+--------------------------------------------------------------+
| SaleType                         | SaleType                                                     |
|                                  |                                                              |
|                                  | * Normal：一般方式(現貨銷售)                                 |
|                                  | * PreSaleByShipDate：DATE 預購 by shipDate(指定出貨日期)     |
|                                  | * PreSaleByShipdays：DAYS 預購 by shipdays(訂購後多少天出貨) |
+----------------------------------+--------------------------------------------------------------+
| CustomizedProductId              | 自定貨號                                                     |
+----------------------------------+--------------------------------------------------------------+
| ProductName                      | 商品名稱                                                     |
|                                  |                                                              |
|                                  | 注意:當ProductName=物流服務費,此訂單不需要執行出貨確認       |
+----------------------------------+--------------------------------------------------------------+
| Spec                             | 商品規格                                                     |
+----------------------------------+--------------------------------------------------------------+
| Amount                           | 數量                                                         |
+----------------------------------+--------------------------------------------------------------+
| Subtotal                         | 金額小計(折扣後價格)                                         |
+----------------------------------+--------------------------------------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "Transaction":
        {
            "@Id":"5475153",
            "DeliveryReceipt":
            {
                "@Id":"10016380",
                "StoreType":"7-11",
                "SerialNumber":"16379",
                "DeliveryReceiptPrice":"1590",
                "DistributionChannelStatus":"0",
                "_DistributionChannelStatusDesc":
                "\u7522\u751f\u51fa\u8ca8\u55ae",
                "OrderShippingConfirmDate":"2010/09/23",
                "LastDeliveryDate":"2010/09/24",
                "OrderDelayShippingDate":"2010/09/28",
                "_ReceiverName":"\u738b\u5c0f\u660e",
                "_TakeDeliveryConvenienceStoreName":"\u5143\u5927\u9580\u5e02",
                "TakeDeliveryConvenienceStoreId":"976253",
                "Barcode":"97625391500610016380",
                "DeliveryToConvenienceStoreDate":"2010/09/25",
                "ConvenienceStoreReturnDate":"2010/10/02",
                "_ConvenienceStoreOrderId":"5475153-16379",
                "_StoreName":"B\u5546\u5e97",
                "_CustomerCareInfo":"02123456789",
                "_Url":"http://tw.mall.yahoo.com",
                "OrderList":
                [
                    {
                        "@Count":"1",
                        "Order":
                        [
                            {
                                "@Id":"YM1008020000008",
                                "OrderStatus":"NEW",
                                "_OrderStatusDesc":"\u672a\u7d50\u6848",
                                "OrderDate":"1900/01/01",
                                "OrderProductList":
                                {
                                    "@Count":"1",
                                    "Product":
                                    [
                                        {
                                            "@Id":"100_1",
                                            "SaleType":"Normal",
                                            "_CustomizedProductId":"A0001\u4e3b\u4ef6100_1",
                                            "_ProductName":"\u4e3b\u4ef6\u4e00",
                                            "_Spec":"",
                                            "Amount":"2",
                                            "Subtotal":"1590"
                                        }
                                    ]
                                }
                            }
                        ]
                    }
                ]
            }
        }
    }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
    <Transaction Id="5475153">
        <DeliveryReceipt Id="10016380">
            <StoreType>7-11</StoreType>
            <SerialNumber>16379</SerialNumber>
            <DeliveryReceiptPrice>1590</DeliveryReceiptPrice>
            <DistributionChannelStatus>0</DistributionChannelStatus>
            <DistributionChannelStatusDesc><![CDATA[產生出貨單]]></DistributionChannelStatusDesc>
            <OrderShippingConfirmDate>2010/09/23</OrderShippingConfirmDate>
            <LastDeliveryDate>2010/09/24</LastDeliveryDate>
            <OrderDelayShippingDate>2010/09/28</OrderDelayShippingDate>
            <ReceiverName><![CDATA[王小明]]></ReceiverName>
            <TakeDeliveryConvenienceStoreName><![CDATA[元大門市]]></TakeDeliveryConvenienceStoreName>
            <TakeDeliveryConvenienceStoreId>976253</TakeDeliveryConvenienceStoreId>
            <Barcode>97625391500610016380</Barcode>
            <DeliveryToConvenienceStoreDate>2010/09/25</DeliveryToConvenienceStoreDate>
            <ConvenienceStoreReturnDate>2010/10/02</ConvenienceStoreReturnDate>
            <ConvenienceStoreOrderId><![CDATA[5475153-16379]]></ConvenienceStoreOrderId>
            <StoreName><![CDATA[B商店]]></StoreName>
            <CustomerCareInfo><![CDATA[02123456789]]></CustomerCareInfo>
            <Url><![CDATA[http://tw.mall.yahoo.com]]></Url>
            <OrderList Count="1">
                <Order Id="YM1008020000008">
                    <OrderStatus>NEW</OrderStatus>
                    <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
                    <OrderDate>1900/01/01</OrderDate>
                    <OrderProductList Count="1">
                        <Product Id="100_1">
                            <SaleType>Normal</SaleType>
                            <CustomizedProductId><![CDATA[A0001主件100_1]]></CustomizedProductId>
                            <ProductName><![CDATA[主件一]]></ProductName>
                            <Spec><![CDATA[]]></Spec>
                            <Amount>2</Amount>
                            <Subtotal>1590</Subtotal>
                        </Product>
                    </OrderProductList>
                </Order>
            </OrderList>
        </DeliveryReceipt>
    </Transaction>
</Response>
```

### Errors

---

/v1/OrderShipping/Confirm&shy;Store&shy;Delivery
--------------------------------------

對超商訂單執行出貨確認(物流交寄)

### Request parameters

+---------------+-----------------+------------------------------------------------------------------------------------+
| Parameter     | Value           | Description                                                                        |
+===============+=================+====================================================================================+
| TransactionId | string(Require) | 交易序號                                                                           |
+---------------+-----------------+------------------------------------------------------------------------------------+
| OrderId       | string(Require) | 訂單編號，可接受多筆，但須屬於同一個交易序號下的訂單編號                           |
|               |                 |                                                                                    |
|               |                 | ex. `TransactionId=T123456&OrderId=O1234567&OrderId=Y123457&OrderId=E123456`       |
|               |                 |                                                                                    |
|               |                 | 請注意：                                                                           |
|               |                 |                                                                                    |
|               |                 | 1.  "物流服務費“不須執行出貨確認(系統會依此[交易序號]之第一筆出貨確認之出貨單出貨) |
|               |                 |                                                                                    |
|               |                 | 2.  傳入之訂單總金額需>0                                                           |
+---------------+-----------------+------------------------------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/ConfirmStoreDelivery?TransactionId=23000&OrderId=YM1234567890123&OrderId=YM1234567890124&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/ConfirmStoreDelivery?TransactionId=23000&OrderId=YM1234567890123&OrderId=YM1234567890124&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+--------------------------------+-----------------------------------+
| Field                          | Description                       |
+================================+===================================+
| StoreType                      | 超商種類                          |
|                                |                                   |
|                                | * 7-11：7-11(統一超商)            |
|                                | * Family：全家超商                |
|                                | * HiLife：萊爾富超商              |
|                                | * None：未使用超商                |
+--------------------------------+-----------------------------------+
| DeliveryReceiptId              | 出貨單編號                        |
+--------------------------------+-----------------------------------+
| DeliveryReceiptPrice           | 出貨單金額                        |
+--------------------------------+-----------------------------------+
| OrderShippingConfirmDate       | 出貨確認日                        |
+--------------------------------+-----------------------------------+
| LastDeliveryDate               | 最晚送貨日                        |
+--------------------------------+-----------------------------------+
| OrderDelayShippingDate         | 可以延遲出貨日                    |
+--------------------------------+-----------------------------------+
| DeliveryToConvenienceStoreDate | 門市進貨日（貨品抵達門市日期）    |
+--------------------------------+-----------------------------------+
| ConvenienceStoreReturnDate     | 門市退貨日（門市退回貨品日期）    |
+--------------------------------+-----------------------------------+
| OrderList                      | 包含此筆出貨單的OrderList，屬性： |
|                                |                                   |
|                                | * Count：資料筆數                 |
+--------------------------------+-----------------------------------+
| Order                          | 包含一筆Order的資料，屬性：       |
|                                |                                   |
|                                | * Id：訂單編號                    |
+--------------------------------+-----------------------------------+
| ErrorCode                      | 錯誤代碼                          |
+--------------------------------+-----------------------------------+
| ErrorMessage                   | 錯誤訊息                          |
+--------------------------------+-----------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "DeliveryReceipt":
        {
            "@Id":"10016380",
            "StoreType":"7-11",
            "DeliveryReceiptPrice":"1590",
            "OrderShippingConfirmDate":"2010/09/23",
            "LastDeliveryDate":"2010/09/24",
            "OrderDelayShippingDate":"2010/09/28",
            "DeliveryToConvenienceStoreDate":"2010/09/25",
            "ConvenienceStoreReturnDate":"2010/10/02",
            "OrderList":
            [
                {
                    "Order":
                    [
                        {
                            "@Id":"YM1008020000008"
                        },
                        {
                            "@Id":"YM1008020000009"
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
    <DeliveryReceipt Id="10016380">
        <StoreType>7-11</StoreType>
        <DeliveryReceiptPrice>1590</DeliveryReceiptPrice>
        <OrderShippingConfirmDate>2010/09/23</OrderShippingConfirmDate>
        <LastDeliveryDate>2010/09/24</LastDeliveryDate>
        <OrderDelayShippingDate>2010/09/28</OrderDelayShippingDate>
        <DeliveryToConvenienceStoreDate>2010/09/25</DeliveryToConvenienceStoreDate>
        <ConvenienceStoreReturnDate>2010/10/02</ConvenienceStoreReturnDate>
        <OrderList>
            <Order Id="YM1008020000008"></Order>
            <Order Id="YM1008020000009"></Order>
        </OrderList>
    </DeliveryReceipt>
</Response>
```

### Errors

+-----------+--------------------------------------+
| ErrorCode | ErrorMessage                         |
+===========+======================================+
| 2121      | 部分訂單不屬此交易序號               |
+-----------+--------------------------------------+
| 2122      | 出貨金額不可=0                       |
+-----------+--------------------------------------+
| 2123      | 請勿傳入物流服務費                   |
+-----------+--------------------------------------+
| 2124      | 部分訂單已出貨，請再確認             |
+-----------+--------------------------------------+
| 2125      | 部分訂單已取消，請再確認             |
+-----------+--------------------------------------+
| 2127      | 無法取得店家資料                     |
+-----------+--------------------------------------+
| 2128      | 訂單無法出貨，請再確認。             |
+-----------+--------------------------------------+
| 2129      | 門市關轉OR店號轉換，請隔日再試行出貨 |
+-----------+--------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/OrderShipping/ConfirmStore&shy;DeliveryC2C
-----------------------------------------

對超商訂單執行出貨確認(門市交寄)

### Request parameters

+---------------+-----------------+------------------------------------------------------------------------------------+
| Parameter     | Value           | Description                                                                        |
+===============+=================+====================================================================================+
| TransactionId | string(Require) | 交易序號                                                                           |
+---------------+-----------------+------------------------------------------------------------------------------------+
| OrderId       | string(Require) | 訂單編號，可接受多筆，但須屬於同一個交易序號下的訂單編號                           |
|               |                 |                                                                                    |
|               |                 | ex. `TransactionId=T123456&OrderId=O1234567&OrderId=Y123457&OrderId=E123456`       |
|               |                 |                                                                                    |
|               |                 | 請注意：                                                                           |
|               |                 |                                                                                    |
|               |                 | 1.  "物流服務費“不須執行出貨確認(系統會依此[交易序號]之第一筆出貨確認之出貨單出貨) |
|               |                 |                                                                                    |
|               |                 | 2.  傳入之訂單總金額需>0                                                           |
+---------------+-----------------+------------------------------------------------------------------------------------+
| SenderName    | string(Require) | 寄件人姓名                                                                         |
+---------------+-----------------+------------------------------------------------------------------------------------+
| SenderMobile  | string(Require) | 寄件人手機                                                                         |
+---------------+-----------------+------------------------------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/ConfirmStoreDeliveryC2C?TransactionId=23000&OrderId=YM1234567890123&OrderId=YM1234567890124&SenderName=seller&SenderMobile=0911222333&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/ConfirmStoreDeliveryC2C?TransactionId=23000&OrderId=YM1234567890123&OrderId=YM1234567890124&SenderName=seller&SenderMobile=0911222333&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+--------------------------------+-----------------------------------+
| Field                          | Description                       |
+================================+===================================+
| StoreType                      | 超商種類                          |
|                                |                                   |
|                                | * 7-11：7-11(統一超商)            |
|                                | * Family：全家超商                |
|                                | * HiLife：萊爾富超商              |
|                                | * None：未使用超商                |
+--------------------------------+-----------------------------------+
| DeliveryReceiptId              | 出貨單編號                        |
+--------------------------------+-----------------------------------+
| DeliveryReceiptPrice           | 出貨單金額                        |
+--------------------------------+-----------------------------------+
| OrderShippingConfirmDate       | 出貨確認日                        |
+--------------------------------+-----------------------------------+
| LastDeliveryDate               | 最晚送貨日                        |
+--------------------------------+-----------------------------------+
| OrderDelayShippingDate         | 可以延遲出貨日                    |
+--------------------------------+-----------------------------------+
| DeliveryToConvenienceStoreDate | 門市進貨日（貨品抵達門市日期）    |
+--------------------------------+-----------------------------------+
| ConvenienceStoreReturnDate     | 門市退貨日（門市退回貨品日期）    |
+--------------------------------+-----------------------------------+
| OrderList                      | 包含此筆出貨單的OrderList，屬性： |
|                                |                                   |
|                                | * Count：資料筆數                 |
+--------------------------------+-----------------------------------+
| Order                          | 包含一筆Order的資料，屬性：       |
|                                |                                   |
|                                | * Id：訂單編號                    |
+--------------------------------+-----------------------------------+
| ErrorCode                      | 錯誤代碼                          |
+--------------------------------+-----------------------------------+
| ErrorMessage                   | 錯誤訊息                          |
+--------------------------------+-----------------------------------+

### Sample response

#### JSON sample

```
{"Response":
    {
        "@Status":"ok",
        "DeliveryReceipt":
        {
            "@Id":"10016380",
            "StoreType":"7-11",
            "DeliveryReceiptPrice":"1590",
            "OrderShippingConfirmDate":"2010/09/23",
            "LastDeliveryDate":"2010/09/24",
            "OrderDelayShippingDate":"2010/09/28",
            "DeliveryToConvenienceStoreDate":"2010/09/25",
            "ConvenienceStoreReturnDate":"2010/10/02",
            "OrderList":
            [
                {
                    "Order":
                    [
                        {
                            "@Id":"YM1008020000008"
                        },
                        {
                            "@Id":"YM1008020000009"
                        }
                    ]
                }
            ]
        }
    }
}
```

### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
    <DeliveryReceipt Id="10016380">
        <StoreType>7-11</StoreType>
        <DeliveryReceiptPrice>1590</DeliveryReceiptPrice>
        <OrderShippingConfirmDate>2010/09/23</OrderShippingConfirmDate>
        <LastDeliveryDate>2010/09/24</LastDeliveryDate>
        <OrderDelayShippingDate>2010/09/28</OrderDelayShippingDate>
        <DeliveryToConvenienceStoreDate>2010/09/25</DeliveryToConvenienceStoreDate>
        <ConvenienceStoreReturnDate>2010/10/02</ConvenienceStoreReturnDate>
        <OrderList>
            <Order Id="YM1008020000008"></Order>
            <Order Id="YM1008020000009"></Order>
        </OrderList>
    </DeliveryReceipt>
</Response>
```

### Errors

+-----------+--------------------------------------+
| ErrorCode | ErrorMessage                         |
+===========+======================================+
| 2121      | 部分訂單不屬此交易序號               |
+-----------+--------------------------------------+
| 2122      | 出貨金額不可=0                       |
+-----------+--------------------------------------+
| 2123      | 請勿傳入物流服務費                   |
+-----------+--------------------------------------+
| 2124      | 部分訂單已出貨，請再確認             |
+-----------+--------------------------------------+
| 2125      | 部分訂單已取消，請再確認             |
+-----------+--------------------------------------+
| 2127      | 無法取得店家資料                     |
+-----------+--------------------------------------+
| 2128      | 訂單無法出貨，請再確認。             |
+-----------+--------------------------------------+
| 2129      | 門市關轉OR店號轉換，請隔日再試行出貨 |
+-----------+--------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/OrderShipping/CancelStore&shy;DeliveryReceipt
-------------------------------------------------

取消超商出貨單

### Request parameters

+-------------------+-----------------+-------------+
| Parameter         | Value           | Description |
+===================+=================+=============+
| DeliveryReceiptId | string(Require) | 出貨單編號  |
+-------------------+-----------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/CancelStoreDeliveryReceipt?DeliveryReceiptId=1234567&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/CancelStoreDeliveryReceipt?DeliveryReceiptId=1234567&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------+---------------------------------------+
| Field           | Description                           |
+=================+=======================================+
| SuccessList     | 成功的出貨單列表                      |
+-----------------+---------------------------------------+
| DeliveryReceipt | 包含一筆DeliveryReceipt的資料，屬性： |
|                 |                                       |
|                 | * Id：出貨單編號                      |
+-----------------+---------------------------------------+
| OrderList       | 包含此筆出貨單的OrderList，屬性：     |
|                 |                                       |
|                 | * Count：資料筆數                     |
+-----------------+---------------------------------------+
| Order           | 包含一筆Order的資料，屬性：           |
|                 |                                       |
|                 | * Id：訂單編號                        |
+-----------------+---------------------------------------+
| ErrorCode       | 錯誤代碼                              |
+-----------------+---------------------------------------+
| ErrorMessage    | 錯誤訊息                              |
+-----------------+---------------------------------------+

### Sample response

#### JSON sample

```
{
    "Response":
    {
        "@Status":"ok",
        "SuccessList":
        {
            "DeliveryReceipt":
            {
                "@Id":"123456",
                "OrderList":
                {
                   "@Count":2,
                   "Order":
                   [
                       {
                           "@Id":"YM1008020000010"
                       },
                       {
                          "@Id":"YM1008020000011"
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
<?xml version="1.0" encoding="UTF-8"?><Response Status="ok">
<SuccessList>
    <DeliveryReceipt Id="123456">
        <OrderList Count="2">
            <Order Id="YM1008020000010"></Order>
            <Order Id="YM1008020000011"></Order>
        </OrderList>
    </DeliveryReceipt>
</SuccessList>
</Response>
```

### Errors

+-----------+--------------------------------------+
| ErrorCode | ErrorMessage                         |
+===========+======================================+
| 2141      | 無法重新包裝：最晚送貨日需大於系統日 |
+-----------+--------------------------------------+
| 2142      | 無法重新包裝，請再確認。             |
+-----------+--------------------------------------+
|           | 已交寄無法作廢。                     |
+-----------+--------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/OrderShipping/ConfirmESD
----------------------------

對ESD訂單執行出貨確認

### Request parameters

+--------------------+------------------+----------------------------------------------------------------------------------------------+
| Parameter          | Value            | Description                                                                                  |
+====================+==================+==============================================================================================+
| TransactionId      | string(Require)  | 交易序號                                                                                     |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| OrderId            | string(Require)  | 訂單編號                                                                                     |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| ProductId.n        | string(Require)  | 商品編號_商品規格編號                                                                        |
|                    |                  |                                                                                              |
|                    |                  | 請將parameter中的"n"以數字代換，ex：ProductId.1=p1020128060_1&ProductId.2=p1020128061_1      |
|                    |                  |                                                                                              |
|                    |                  | 1.  "物流服務費“不須執行出貨確認                                                             |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| DownloadSite.n     | string(Optional) | 下載網址                                                                                     |
|                    |                  |                                                                                              |
|                    |                  | 請將parameter中的"n"以數字代換，n為對應ProductId.n所屬的資料內容                             |
|                    |                  |                                                                                              |
|                    |                  | 若未傳入則default=商店首頁                                                                   |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| DownloadSiteNote.n | string(Optional) | 下載網址說明                                                                                 |
|                    |                  |                                                                                              |
|                    |                  | 請將parameter中的"n"以數字代換，n為對應ProductId.n所屬的資料內容                             |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| ProductKey.n       | string(Optional) | 商品序號                                                                                     |
|                    |                  |                                                                                              |
|                    |                  | 請將parameter中的"n"以數字代換，n為對應ProductId.n所屬的資料內容                             |
|                    |                  |                                                                                              |
|                    |                  | 1.  若未傳入則default=店家另行發送                                                           |
|                    |                  |                                                                                              |
|                    |                  | 2.  "若傳入需符合購買數量 (可同時傳入多筆)                                                   |
|                    |                  |                                                                                              |
|                    |                  |     ex: 若買了2個ProductId.1的商品，則需傳入兩個序號                                         |
|                    |                  |     ProductKey.1=itemkey1&ProductKey.1=itemkey2                                              |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| ShippingNote       | string(Optional) | 出貨備註                                                                                     |
+--------------------+------------------+----------------------------------------------------------------------------------------------+
| OthersEmail        | string(Optional) | 其他Email                                                                                    |
|                    |                  |                                                                                              |
|                    |                  | 1.  "若未傳入則default=若傳入則僅會寄至此Email地址                                           |
+--------------------+------------------+----------------------------------------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/OrderShipping/ConfirmESD?TransactionId=23000&OrderId=YM1234567890123&ProductId.1=p1234567890_1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/OrderShipping/ConfirmESD?TransactionId=23000&OrderId=YM1234567890123&ProductId.1=p1234567890_1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+--------------------------+-------------+
| Field                    | Description |
+==========================+=============+
| OrderShippingConfirmDate | 出貨確認日  |
+--------------------------+-------------+
| ErrorCode                | 錯誤代碼    |
+--------------------------+-------------+
| ErrorMessage             | 錯誤訊息    |
+--------------------------+-------------+

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
        "OrderShippingConfirmDate": "2010/11/12"
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
                  <OrderShippingConfirmDate>2010/11/12</OrderShippingConfirmDate>
            </Order>
      </Transaction>
</Response>
```

### Errors

+-----------+--------------------------+
| ErrorCode | ErrorMessage             |
+===========+==========================+
| 2151      | 此為[物流服務費]無需出貨 |
+-----------+--------------------------+
| 2152      | [商品編號]筆數不符       |
+-----------+--------------------------+
| 2153      | 傳入[商品編號]無效       |
+-----------+--------------------------+
| 2154      | [商品序號]筆數不符       |
+-----------+--------------------------+
| 2155      | 供應商不存在             |
+-----------+--------------------------+
| 2156      | 訂單非未出貨狀態         |
+-----------+--------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)
