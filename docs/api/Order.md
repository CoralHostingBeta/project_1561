/v1/Order/Query
---------------

訂單查詢,可依據不同的條件查詢訂單列表

### Request parameters

+--------------+--------------------+-----------------------------------+
| Parameter    | Value              | Description                       |
+==============+====================+===================================+
| OrderType    | string(20/Require) | 訂單類型                          |
|              |                    |                                   |
|              |                    | * All:全部                        |
|              |                    | * NonShipping:未出貨              |
|              |                    | * Shipping:已出貨                 |
|              |                    | * NonClose:未結案                 |
|              |                    | * Closed:已結案                   |
+--------------+--------------------+-----------------------------------+
| ShippingType | string(20/Require) | 配送方式                          |
|              |                    |                                   |
|              |                    | * HomeDelivery:宅配               |
|              |                    | * StoreDelivery:超商              |
|              |                    | * ESD:電子下載                    |
+--------------+--------------------+-----------------------------------+
| DateType     | string(20/Require) | 日期條件                          |
|              |                    |                                   |
|              |                    | * TransferDate:轉單日             |
|              |                    | * LastShippingDate:最晚出貨日     |
|              |                    | * OrderCloseDate:訂單結案日       |
+--------------+--------------------+-----------------------------------+
| StartDate    | date(Require)      | 起始日期                          |
|              |                    |                                   |
|              |                    | 第一種格式（yyyy/mm/dd）          |
|              |                    |                                   |
|              |                    | 第二種格式（yyyy/mm/dd hh:mm:ss） |
+--------------+--------------------+-----------------------------------+
| EndDate      | date(Require)      | 迄止日期                          |
|              |                    |                                   |
|              |                    | 第一種格式（yyyy/mm/dd）          |
|              |                    |                                   |
|              |                    | 第二種格式（yyyy/mm/dd hh:mm:ss） |
|              |                    |                                   |
|              |                    | EndDate-StartDate 要小於等於7天   |
+--------------+--------------------+-----------------------------------+
| Position     | int(Require)       | 由第幾筆開始拿資料                |
+--------------+--------------------+-----------------------------------+
| Count        | int(Require)       | 資料筆數                          |
|              |                    |                                   |
|              |                    | Count=1~100                       |
+--------------+--------------------+-----------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/Query?OrderType=All&ShippingType=HomeDelivery&DateType=TransferDate&StartDate=2010/01/01&EndDate=2010/01/02&Position=1&Count=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/Query?OrderType=All&ShippingType=HomeDelivery&DateType=TransferDate&StartDate=2010/01/01&EndDate=2010/01/02&Position=1&Count=1&Format=xml
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
| (string/15)     |                                            |
|                 | * Id ：交易序號                            |
+-----------------+--------------------------------------------+
| Order           | 訂單編號                                   |
| (string/20)     |                                            |
|                 | * Id: 訂單編號                             |
+-----------------+--------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "TransactionList": {
      "@Count": 3,
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
   <TransactionList Count="3" TotalCount="10">
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

/v1/Order/QueryNonPayment
-------------------------

查詢未付款完成的訂單

### Request parameters

+----------------+-----------------+--------------------------------------------+
| Parameter      | Value           | Description                                |
+================+=================+============================================+
| StartOrderDate | date(Require)   | 訂購起始日期                               |
|                |                 |                                            |
|                |                 | （yyyy/mm/dd）                             |
+----------------+-----------------+--------------------------------------------+
| EndOrderDate   | date(Require)   | 訂購迄止日期                               |
|                |                 |                                            |
|                |                 | （yyyy/mm/dd）                             |
|                |                 |                                            |
|                |                 | EndOrderDate-StartOrderDate必須小於等於3天 |
+----------------+-----------------+--------------------------------------------+
| ShippingType   | string          | 配送方式                                   |
|                | (Require/20)    |                                            |
|                |                 | * HomeDelivery：宅配                       |
|                |                 | * StoreDelivery：超商                      |
|                |                 | * ESD：電子下載                            |
+----------------+-----------------+--------------------------------------------+
| OrderStatus    | String          | 訂單狀態                                   |
|                | (Require/20)    |                                            |
|                |                 | * ALL:全部                                 |
|                |                 | * NEW:未結案                               |
|                |                 | * CANCEL:取消                              |
+----------------+-----------------+--------------------------------------------+
| Position       | int(Require)    | 由第幾筆開始拿資料                         |
+----------------+-----------------+--------------------------------------------+
| Count          | int(Require)    | 資料筆數                                   |
|                |                 |                                            |
|                |                 | Count=1~100                                |
+----------------+-----------------+--------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/QueryNonPayment?ShippingType=HomeDelivery&StartOrderDate=2010/01/01&EndOrderDate=2010/01/02&OrderStatus=ALL&Position=1&Count=1&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/QueryNonPayment?ShippingType=HomeDelivery&StartOrderDate=2010/01/01&EndOrderDate=2010/01/02&OrderStatus=ALL&Position=1&Count=1&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+---------------------+--------------------------------------------------------------+
| Field               | Description                                                  |
+=====================+==============================================================+
| TransactionList     | 包含符合查詢條件的Transaction List，屬性：                   |
|                     |                                                              |
|                     | * Count：資料筆數                                            |
+---------------------+--------------------------------------------------------------+
| TotalCount          | 符合查詢條件的總資料筆數                                     |
+---------------------+--------------------------------------------------------------+
| Transaction         | 包含一筆Transaction的資料，屬性：                            |
| (string/15)         |                                                              |
|                     | * Id：交易序號                                               |
+---------------------+--------------------------------------------------------------+
| BuyerName           | 訂購人姓名                                                   |
| (string/20)         |                                                              |
+---------------------+--------------------------------------------------------------+
| PayType             | 此筆交易使用的付款方式                                       |
| (string/20)         |                                                              |
|                     | * CreditCard：信用卡                                         |
|                     | * ATM：ATM                                                   |
|                     | * StorePay：超商繳費（IBON/FAMI）                            |
|                     | * StoreDelivery：超商付款取貨                                |
+---------------------+--------------------------------------------------------------+
| ShippingType        | 此筆交易使用的配送方式                                       |
| (string/20)         |                                                              |
|                     | * HomeDelivery：宅配                                         |
|                     | * StoreDelivery：超商                                        |
|                     | * ESD：ESD                                                   |
+---------------------+--------------------------------------------------------------+
| Order               | 包含ㄧ筆Order的資料，屬性：                                  |
| (string/20)         |                                                              |
|                     | * Id：訂單編號                                               |
+---------------------+--------------------------------------------------------------+
| OrderStatus         | 訂單狀態                                                     |
| (string/20)         |                                                              |
|                     | * NEW：未結案                                                |
|                     | * CANCEL：取消                                               |
+---------------------+--------------------------------------------------------------+
| DeliverType         | 交寄方式                                                     |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| OrderNote           | 訂單備註                                                     |
| (string/150)        |                                                              |
+---------------------+--------------------------------------------------------------+
| OrderStatusDesc     | 訂單狀態描述                                                 |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| OrderDate           | 訂購日                                                       |
+---------------------+--------------------------------------------------------------+
| OrderProductList    | 包含OrderList，屬性：                                        |
|                     |                                                              |
|                     | * Count：資料筆數                                            |
+---------------------+--------------------------------------------------------------+
| Product             | 包含一筆訂購的商品資料，屬性：                               |
|  (string/16)        |                                                              |
|                     | * Id：商品編號                                               |
+---------------------+--------------------------------------------------------------+
| SaleType            | SaleType                                                     |
| (string/20)         |                                                              |
|                     | * Normal：一般方式(現貨銷售)                                 |
|                     | * PreSaleByShipDate：DATE 預購 by shipDate(指定出貨日期)     |
|                     | * PreSaleByShipdays：DAYS 預購 by shipdays(訂購後多少天出貨) |
+---------------------+--------------------------------------------------------------+
| CustomizedProductId | 自訂貨號                                                     |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| ProductName         | 商品名稱                                                     |
| (string/150)        |                                                              |
+---------------------+--------------------------------------------------------------+
| Spec                | 商品規格                                                     |
| (string/50)         |                                                              |
+---------------------+--------------------------------------------------------------+
| Amount              | 數量                                                         |
|  (int)              |                                                              |
+---------------------+--------------------------------------------------------------+
| Subtotal            | 金額小計(折扣後價格)                                         |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+

### Sample response

#### JSON sample

```
{
    "Response":
    {
        "@Status":"ok",
        "TransactionList":
        {
            "@Count":2,
            "@TotalCount":10,
            "Transaction":
            [
                {
                    "@Id":"5473347",
                    "_BuyerName":"\u6e38\u6587\u516d",
                    "PayType":"StorePay(FAMI)",
                    "ShippingType":"HomeDelivery",
                    "OrderList":
                    [
                        {
                            "Order":
                            [
                                {
                                    "@Id":"YM1008020000007",
                                    "OrderStatus":"NEW",
                                    "_OrderStatusDesc":"\u672a\u7d50\u6848",
                                    "OrderDate":"1900/01/01",
                                    "OrderProductList":
                                    {
                                         "@Count":"1",
                                         "Product":
                                         [
                                             {
                                                 "@Id":"1020623",
                                                 "SaleType":"Normal",
                                                 "_CustomizedProductId":"",
                                                 "_ProductName":"\u7269\u6d41\u670d\u52d9\u8cbb",
                                                 "_Spec":"",
                                                 "Amount":"1",
                                                 "Subtotal":"80"
                                             }
                                         ]
                                    }
                                },
                                {
                                    "@Id":"YM1008020000008",
                                    "OrderStatus":"NEW",
                                    "_OrderStatusDesc":"\u672a\u7d50\u6848",
                                    "OrderDate":"1900/01/01",
                                    "OrderProductList":
                                    {
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
                },
                {
                    "@Id":"5473348",
                    "_BuyerName":"\u6e38\u6587\u516d",
                    "PayType":"CreditCard",
                    "ShippingType":"HomeDelivery",
                    "OrderList":
                    [
                        {
                            "Order":
                            [
                                {
                                    "@Id":"YM1008020000007",
                                    "OrderStatus":"NEW",
                                    "_OrderStatusDesc":"\u672a\u7d50\u6848",
                                    "OrderDate":"1900/01/01",
                                    "OrderProductList":
                                    {
                                        "@Count":"1",
                                        "Product":
                                        [
                                            {
                                                "@Id":"1020623",
                                                "SaleType":"Normal",
                                                "_CustomizedProductId":"",
                                                "_ProductName":"\u7269\u6d41\u670d\u52d9\u8cbb",
                                                "_Spec":"",
                                                "Amount":"1",
                                                "Subtotal":"80"
                                            }
                                        ]
                                    }
                                },
                                {
                                    "@Id":"YM1008020000009",
                                    "OrderStatus":"Cancel",
                                    "_OrderStatusDesc":"\u53d6\u6d88-\u5584\u610f-\u4e0d\u7f70",
                                    "OrderDate":"1900/01/01",
                                    "OrderProductList":
                                    {
                                        "Product":
                                        [
                                            {
                                                "@Id":"1020623",
                                                "SaleType":"Normal",
                                                "_CustomizedProductId":"",
                                                "_ProductName":"\u7269\u6d41\u670d\u52d9\u8cbb",
                                                "_Spec":"",
                                                "Amount":"1",
                                                "Subtotal":"80"
                                            }
                                        ]
                                    }
                                },
                                {
                                    "@Id":"YM1008020000010",
                                    "OrderStatus":"CANCEL",
                                    "_OrderStatusDesc":"\u53d6\u6d88-\u5584\u610f-\u4e0d\u7f70",
                                    "OrderDate":"1900/01/01",
                                    "OrderProductList":
                                    {"Product":
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
    <Transaction Id="5473347">
      <BuyerName><![CDATA[游文六]]></BuyerName>
      <PayType>StorePay(FAMI)</PayType>
      <ShippingType>HomeDelivery</ShippingType>
      <OrderList>
        <Order Id="YM1008020000007">
          <OrderStatus>NEW</OrderStatus>
          <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
          <OrderDate>1900/01/01</OrderDate>
          <OrderProductList Count="1">
            <Product Id="1020623">
              <SaleType>Normal</SaleType>
              <CustomizedProductId><![CDATA[]]></CustomizedProductId>
              <ProductName><![CDATA[物流服務費]]></ProductName>
              <Spec><![CDATA[]]></Spec>
              <Amount>1</Amount>
              <Subtotal>80</Subtotal>
            </Product>
          </OrderProductList>
        </Order>
        <Order Id="YM1008020000008">
          <OrderStatus>NEW</OrderStatus>
          <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
          <OrderDate>1900/01/01</OrderDate>
          <OrderProductList>
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
    </Transaction>
    <Transaction Id="5473348">
      <BuyerName><![CDATA[游文六]]></BuyerName>
      <PayType>CreditCard</PayType>
      <ShippingType>HomeDelivery</ShippingType>
      <OrderList>
        <Order Id="YM1008020000007">
          <OrderStatus>NEW</OrderStatus>
          <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
          <OrderDate>1900/01/01</OrderDate>
          <OrderProductList Count="1">
            <Product Id="1020623">
              <SaleType>Normal</SaleType>
              <CustomizedProductId><![CDATA[]]></CustomizedProductId>
              <ProductName><![CDATA[物流服務費]]></ProductName>
              <Spec><![CDATA[]]></Spec>
              <Amount>1</Amount>
              <Subtotal>80</Subtotal>
            </Product>
          </OrderProductList>
        </Order>
        <Order Id="YM1008020000009">
          <OrderStatus>Cancel</OrderStatus>
          <OrderStatusDesc>
            <![CDATA[取消-善意-不罰]]>
            </OrderStatusDesc>
          <OrderDate>1900/01/01</OrderDate>
          <OrderProductList>
            <Product Id="1020623">
              <SaleType>Normal</SaleType>
              <CustomizedProductId>
                <![CDATA[]]>
                </CustomizedProductId>
              <ProductName>
                <![CDATA[物流服務費]]>
                </ProductName>
              <Spec>
                <![CDATA[]]>
                </Spec>
              <Amount>1</Amount>
              <Subtotal>80</Subtotal>
            </Product>
          </OrderProductList>
        </Order>
        <Order Id="YM1008020000010">
          <OrderStatus>CANCEL</OrderStatus>
          <OrderStatusDesc><![CDATA[取消-善意-不罰]]></OrderStatusDesc>
          <OrderDate>1900/01/01</OrderDate>
          <OrderProductList>
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
    </Transaction>
  </TransactionList>
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
| 2109      | 無資料                             |
+-----------+------------------------------------+
| 2110      | 物流商代碼不存在                   |
+-----------+------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Order/GetStatus
-------------------

查詢訂單狀態

### Request parameters

+---------------+------------------+---------------------------------------------------------------+
| Parameter     | Value            | Description                                                   |
+===============+==================+===============================================================+
| TransactionId | string           | 交易序號                                                      |
|               |(Require/15)      |                                                               |
+---------------+------------------+---------------------------------------------------------------+
| OrderId       | string           | 訂單編號                                                      |
|               |(Require/20)      |                                                               |
|               |                  | 一次可select同一個TransactionId下的多個OrderId，最大接受100個 |
|               |                  |                                                               |
|               |                  | ex：TransactionId=23000&OrderId=2300001&OrderId=2300002       |
+---------------+------------------+---------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/GetStatus?TransactionId=23000&OrderId=2300001&OrderId=2300002&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/GetStatus?TransactionId=23000&OrderId=2300001&OrderId=2300002&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-----------------+-----------------------------+
| Field           | Description                 |
+=================+=============================+
| Transaction     | 交易序號                    |
| (string/15)     |                             |
+-----------------+-----------------------------+
| SuccessList     | 包含成功的Order資料         |
+-----------------+-----------------------------+
| OrderList       | 包含Order List，屬性：      |
|                 |                             |
|                 | * Count：資料筆數           |
+-----------------+-----------------------------+
| Order           | 包含一筆Order的資料，屬性： |
| (string/20)     |                             |
|                 | * Id：訂單編號              |
+-----------------+-----------------------------+
| OrderStatus     | 訂單狀態                    |
| (string/20)     |                             |
|                 | * NEW:未結案                |
|                 | * CANCEL:取消               |
|                 | * SHIPPED:完成出貨          |
+-----------------+-----------------------------+
| OrderStatusDesc | 訂單狀態描述                |
|(string/30)      |                             |
+-----------------+-----------------------------+
| FailList        | 包含失敗的Order資料         |
+-----------------+-----------------------------+
| OrderList       | 包含Order List，屬性：      |
|                 |                             |
|                 | * Count：資料筆數           |
+-----------------+-----------------------------+
| Order           | 包含一筆Order的資料，屬性： |
| (string/20)     |                             |
|                 | * Id：訂單編號              |
+-----------------+-----------------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
      "@Id": 123456,
      "FailList": {
        "@Count": 3,
        "OrderList": {
         "Order": [
            {
              "@Id": "YM1234577"
            },
            {
              "@Id": "YM1234588"
            },
            {
              "@Id": "YM1234599"
            }
          ]
        }
      },
      "SuccessList": {
        "@Count": 3,
        "OrderList": {
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
            <SuccessList Count="3">
                  <OrderList>
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
                  </OrderList>
            </SuccessList>
            <FailList Count="3">
                  <OrderList>
                        <Order Id="YM1234577"></Order>
                        <Order Id="YM1234588"></Order>
                        <Order Id="YM1234599"></Order>
                  </OrderList>
            </FailList>
      </Transaction>
</Response>
```

### Errors

---

/v1/Order/GetMaster
-------------------

取得購物車資料

### Request parameters

+---------------+------------------+-------------+
| Parameter     | Value            | Description |
+===============+==================+=============+
| TransactionId | string (Require) | 交易序號    |
|               | (Require/15)     |             |
+---------------+------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/GetMaster?TransactionId=21410239&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/GetMaster?TransactionId=21410239&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+-------------------+----------------------------------------------+
| Field             | Description                                  |
+===================+==============================================+
| TransactionId     | 交易序號                                     |
|(string/15)        |                                              |
+-------------------+----------------------------------------------+
| BuyerName         | 訂購人姓名                                   |
|(string/20)        |                                              |
+-------------------+----------------------------------------------+
| BuyerPhone        | 訂購人電話                                   |
|(string/30)        |                                              |
+-------------------+----------------------------------------------+
| IsActivity        | 此筆交易是否有符合活動                       |
|                   |                                              |
|                   | * 有活動：Yes                                |
|                   | * 無活動：No                                 |
+-------------------+----------------------------------------------+
| IsUseCoupon       | 此筆交易是否有使用電子折價券                 |
|                   |                                              |
|                   | * 有使用：Yes                                |
|                   | * 未使用：No                                 |
+-------------------+----------------------------------------------+
| PayType           | 此筆交易使用的付款方式                       |
|(string/20)        |                                              |
|                   | * CreditCard:信用卡                          |
|                   | * ATM:ATM                                    |
|                   | * StorePay:超商繳費(IBON/FAMI)               |
|                   | * StoreDelivery:超商付款取貨                 |
+-------------------+----------------------------------------------+
| Installment       | 分期期數                                     |
|(int)              |                                              |
+-------------------+----------------------------------------------+
| ShippingType      | 此筆交易使用的配送方式                       |
|(string/20)        |                                              |
|                   | * HomeDelivery：宅配                         |
|                   | * StoreDelivery：超商                        |
|                   | * ESD：ESD                                   |
+-------------------+----------------------------------------------+
| StoreType         | 超商種類                                     |
|(string/20)        |                                              |
|                   | 當ShippingType=StoreDelivery時，此欄位才有值 |
|                   |                                              |
|                   | * 7-11：7-11(統一超商)                       |
|                   | * Family：全家超商                           |
|                   | * HiLife：萊爾富超商                         |
|                   | * None：未使用超商                           |
+-------------------+----------------------------------------------+
| StoreShippingType | 物流方式(由商店設定供Buyer使用的物流方式)    |
|(string/30)        |                                              |
+-------------------+----------------------------------------------+
| TransactionRemark | 此筆交易的備註                               |
|(string/150)       |                                              |
+-------------------+----------------------------------------------+
| TransactionPrice  | 此筆交易的總金額                             |
| (int)             |                                              |
+-------------------+----------------------------------------------+
| OrderList         | 包含此筆交易的Order List，屬性：             |
|                   |                                              |
|                   | * Count：資料筆數                            |
+-------------------+----------------------------------------------+
| Order             | 包含一筆Order的資料，屬性：                  |
| (string/20)       |                                              |
|                   | * Id：訂單編號                               |
+-------------------+----------------------------------------------+
| OrderStatus       | 訂單狀態                                     |
|(string/20)        |                                              |
|                   | * NEW:未結案                                 |
|                   | * CANCEL:取消                                |
|                   | * SHIPPED:完成出貨                           |
+-------------------+----------------------------------------------+
| OrderStatusDesc   | 訂單狀態描述                                 |
| (string/30)       |                                              |
+-------------------+----------------------------------------------+
| OrderCloseDate    | 訂單結案日                                   |
+-------------------+----------------------------------------------+
| OrderPackageDate  | 包裝確認日                                   |
+-------------------+----------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
      "@Id": 123456,
      "IsActivity": "Yes",
      "IsUseCoupon": "Yes",
      "OrderList": {
        "Order": [
          {
            "@Id": "YM1511020082582",
            "OrderCloseDate": "2010/11/12",
            "OrderPackageDate": "2010/11/11",
            "OrderStatus": "NEW",
            "OrderStatusDesc": "未結案"
          },
          {
            "@Id": "YM1511020082582",
            "OrderCloseDate": "2010/11/12",
            "OrderPackageDate": "2010/11/11",
            "OrderStatus": "SHIPPED",
            "OrderStatusDesc": "完成出貨"
          },
          {
            "@Id": "YM1511020082583",
            "OrderCloseDate": "2010/11/12",
            "OrderPackageDate": "2010/11/11",
            "OrderStatus": "Cancel",
            "OrderStatusDesc": "取消-缺貨"
          }
        ]
      },
      "PayType": "CreditCard",
      "Installment": "6",
      "ShippingType": "HomeDelivery",
      "StoreType": "None",
      "TransactionPrice": 300,
      "_BuyerName": "\u9673\u7f8e\u7f8e",
      "_BuyerPhone": "0911111111",
      "_TransactionRemark": "\u8acb\u8ddf\u6211\u806f\u7d61"
    }
  }
}
```

#### XML sample

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
      <Transaction Id="123456">
            <OrderList>
                  <Order Id="YM1511020082511">
                        <OrderStatus>NEW</OrderStatus>
                        <OrderStatusDesc>未結案</OrderStatusDesc>
                        <OrderCloseDate>2010/11/12</OrderCloseDate>
                        <OrderPackageDate>2010/11/11</OrderPackageDate>
                  </Order>
                  <Order Id="YM1511020082512">
                        <OrderStatus>SHIPPED</OrderStatus>
                        <OrderStatusDesc>完成出貨</OrderStatusDesc>
                        <OrderCloseDate>2010/11/12</OrderCloseDate>
                        <OrderPackageDate>2010/11/11</OrderPackageDate>
                  </Order>
                  <Order Id="YM1511020082513">                        
                        <OrderStatus>CANCEL</OrderStatus>
                        <OrderStatusDesc>取消-缺貨</OrderStatusDesc>
                        <OrderCloseDate>2010/11/12</OrderCloseDate>
                        <OrderPackageDate>2010/11/11</OrderPackageDate>
                  </Order>
            </OrderList>
            <BuyerName>
                  <![CDATA[陳美美]]>
            </BuyerName>
            <BuyerPhone>
                  <![CDATA[0911111111]]>
            </BuyerPhone>
            <IsActivity>Yes</IsActivity>
            <IsUseCoupon>Yes</IsUseCoupon>
            <PayType>CreditCard</PayType>
            <Installment>6</Installment>
            <ShippingType>HomeDelivery</ShippingType>
            <StoreType>None</StoreType>
            <TransactionRemark>
                  <![CDATA[請跟我聯絡]]>
            </TransactionRemark>
            <TransactionPrice>300</TransactionPrice>
      </Transaction>
</Response>>
```

### Errors

---

/v1/Order/GetDetail
-------------------

取得購物車中訂單明細資料

### Request parameters

+---------------+------------------+---------------------------------------------------------------+
| Parameter     | Value            | Description                                                   |
+===============+==================+===============================================================+
| TransactionId | string           | 交易序號                                                      |
|               |  (Require/15)    |                                                               |
+---------------+------------------+---------------------------------------------------------------+
| OrderId       | string           | 訂單編號                                                      |
|               | (Require/20      |                                                               |
|               |                  | 一次可select同一個TransactionId下的多個OrderId，最大接受100個 |
|               |                  |                                                               |
|               |                  | ex：TransactionId=23000&OrderId=2300001&OrderId=2300002       |
+---------------+------------------+---------------------------------------------------------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/GetDetail?TransactionId=21410239&OrderId=2300001&OrderId=2300002&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/GetDetail?TransactionId=21410239&OrderId=2300001&OrderId=2300002&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+---------------------+--------------------------------------------------------------+
| Field               | Description                                                  |
+=====================+==============================================================+
| TransactionId       | 交易序號                                                     |
| (string/15)         |                                                              |
+---------------------+--------------------------------------------------------------+
| Receiver            | 包含此筆交易的收件者資料                                     |
+---------------------+--------------------------------------------------------------+
| ReceiverName        | 收件者姓名                                                   |
| (string/20)         |                                                              |
+---------------------+--------------------------------------------------------------+
| ReceiverPhone       | 收件者電話                                                   |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| ReceiverMobile      | 收件者手機                                                   |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| ReceiverZipcode     | 收件者郵遞區號                                               |
| (string/5)          |                                                              |
+---------------------+--------------------------------------------------------------+
| ReceiverAddress     | 收件者地址                                                   |
| (string/150)        |                                                              |
+---------------------+--------------------------------------------------------------+
| SuccessList         | 包含成功的Order資料                                          |
+---------------------+--------------------------------------------------------------+
| OrderList           | 包含Order List，屬性：                                       |
|                     |                                                              |
|                     | * Count：資料筆數                                            |
+---------------------+--------------------------------------------------------------+
| Order               | 包含一筆Order的資料，屬性：                                  |
| (string/20)         |                                                              |
|                     | * Id：訂單編號                                               |
+---------------------+--------------------------------------------------------------+
| OrderStatus         | 訂單狀態                                                     |
| (string/20)         |                                                              |
|                     | * NEW:未結案                                                 |
|                     | * CANCEL:取消                                                |
|                     | * SHIPPED:完成出貨                                           |
+---------------------+--------------------------------------------------------------+
| OrderStatusDesc     | 訂單狀態描述                                                 |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| TransferDate        | 轉單日                                                       |
+---------------------+--------------------------------------------------------------+
| LastShippingDate    | 最晚出貨日                                                   |
+---------------------+--------------------------------------------------------------+
| OrderShippingDate   | 店家出貨日                                                   |
+---------------------+--------------------------------------------------------------+
| OrderCloseDate      | 訂單結案日                                                   |
+---------------------+--------------------------------------------------------------+
| BuyerConfirmDate    | 買家確認日                                                   |
+---------------------+--------------------------------------------------------------+
| EntryAccountDate    | 入帳日                                                       |
+---------------------+--------------------------------------------------------------+
| PickingDate         | 揀貨日                                                       |
+---------------------+--------------------------------------------------------------+
| OrderPackageDate    | 包裝確認日                                                   |
+---------------------+--------------------------------------------------------------+
| LastDeliveryDate    | 最晚送貨日                                                   |
+---------------------+--------------------------------------------------------------+
| OrderShippingId     | 出貨單號                                                     |
| (string/25)         |                                                              |
+---------------------+--------------------------------------------------------------+
| InvoiceNo           | 發票號碼                                                     |
| (string/20)         |                                                              |
+---------------------+--------------------------------------------------------------+
| InvoiceDate         | 發票日期                                                     |
+---------------------+--------------------------------------------------------------+
| DeliverType         | 交寄方式                                                     |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| OrderNote           | 訂單備註                                                     |
| (string/150)        |                                                              |
+---------------------+--------------------------------------------------------------+
| OrderProductList    | 包含此筆訂單的Order Product  List，屬性：                    |
|                     |                                                              |
|                     | * Count：資料筆數                                            |
+---------------------+--------------------------------------------------------------+
| Product             | 包含一筆訂購的商品資料，屬性：                               |
| (string/16)         |                                                              |
|                     | * Id：商品編號                                               |
+---------------------+--------------------------------------------------------------+
| ProductType         | 商品型態                                                     |
| (string/10)         |                                                              |
|                     | * Main：主商品                                               |
|                     | * Addon：加購品                                              |
|                     | * Freebie：贈品                                              |
+---------------------+--------------------------------------------------------------+
| SaleType            | SaleType                                                     |
| (string/20)         |                                                              |
|                     | * Normal：一般方式(現貨銷售)                                 |
|                     | * PreSaleByShipDate：DATE 預購 by shipDate(指定出貨日期)     |
|                     | * PreSaleByShipdays：DAYS 預購 by shipdays(訂購後多少天出貨) |
+---------------------+--------------------------------------------------------------+
| CustomizedProductId | 自定貨號                                                     |
| (string/30)         |                                                              |
+---------------------+--------------------------------------------------------------+
| ProductName         | 商品名稱                                                     |
| (string/150)        |                                                              |
|                     | 注意:當ProductName=物流服務費,此訂單不需要執行出貨確認       |
+---------------------+--------------------------------------------------------------+
| Spec                | 商品規格                                                     |
| (string/50)         |                                                              |
+---------------------+--------------------------------------------------------------+
| Amount              | 數量                                                         |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| OriginalPrice       | 購物車內商品單價                                             |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| ListPrice           | 商品頁銷售價格                                               |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| UsedPoint           | 超贈點點數                                                   |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| BasicPointDiscount  | 超贈點折抵金額                                               |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| Subtotal            | 金額小計(折扣後的價格)                                       |
| (int)               |                                                              |
+---------------------+--------------------------------------------------------------+
| TaxType             | 稅別                                                         |
| (string/10)         |                                                              |
|                     | * Taxable：應稅                                              |
|                     | * TaxFree：免稅                                              |
|                     | * NoInv：免發票                                              |
+---------------------+--------------------------------------------------------------+
| FailList            | 包含失敗的Order資料                                          |
+---------------------+--------------------------------------------------------------+
| OrderList           | 包含Order List，屬性：                                       |
|                     |                                                              |
|                     | * Count：資料筆數                                            |
+---------------------+--------------------------------------------------------------+
| Order               | 包含一筆Order的資料，屬性：                                  |
| (string/20)         |                                                              |
|                     | * Id：訂單編號                                               |
+---------------------+--------------------------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "Transaction": {
     "@Id": 123456,
      "Receiver": {
        "_ReceiverAddress": "\u53f0\u5317\u5e02\u58eb\u6797\u5340\u6587\u5316\u8def1\u865f",
        "_ReceiverMobile": "0911111111",
        "_ReceiverName": "\u9673\u7f8e\u7f8e",
        "_ReceiverPhone": "02-22222222",
        "_ReceiverZipcode": "100"
      },
      "SuccessList": {
        "OrderList": {
          "@Count": 2,
          "Order": [
            {
              "@Id": "YM1234577",
              "BuyerConfirmDate": "2010/11/15",
              "OrderCloseDate": "2010/11/16",
              "EntryAccountDate": "2010/11/15",
              "LastShippingDate": "2010/11/15",
              "InvoiceNo": "WE92904105",
              "InvoiveDate": "2010/11/15",
              "OrderProductList": {
                "Product": [
                  {
                    "@Id": "p2345677",
                    "Amount": 2,
                    "OriginalPrice": 52000,
                    "ListPrice": 52000,
                    "UsedPoint", 0,
                    "BasicPointDiscount", 0,
                    "Subtotal": "52000",
                    "TaxType": "Taxable",
                    "ProductType": "Main",
                    "_CustomizedProductId": "A123456",
                    "_ProductName": "iphone 4 \u5168\u914d",
                    "_Spec": "\u9ed1\u8272"
                  },
                  {
                    "@Id": "p23456799",
                    "Amount": 2,
                    "OriginalPrice": 0,
                    "ListPrice": 0,
                    "UsedPoint", 0,
                    "BasicPointDiscount", 0,
                    "Subtotal": "0",
                    "TaxType": "TaxFree",
                    "ProductType": "Main",
                    "_CustomizedProductId": "",
                    "_ProductName": "iphone 4 \u76ae\u5957",
                    "_Spec": "\u767d\u8272"
                  }
                ]
              },
              "OrderPackageDate": "2010/11/14",
              "OrderShippingDate": "2010/11/14",
              "_OrderShippingId": "X123456",
              "PickingDate": "2010/11/14",
              "TransferDate": "2010/11/11",
              "_DeliverType": "自行運送(99)",
              "_OrderNote": "請在03/0803/08早上到貨",
              "_OrderStatus": "NEW",
              "_OrderStatusDesc": "未結案"
            },
            {
              "@Id": "YM1234588",
              "BuyerConfirmDate": "2010/11/15",
              "OrderCloseDate": "2010/11/16",
              "EntryAccountDate": "2010/11/15",
              "LastShippingDate": "2010/11/15",
              "InvoiceNo": "WE92904106",
              "InvoiveDate": "2010/11/15",
              "OrderProductList": {
                "Product": [
                  {
                    "@Id": "p2345999",
                    "Amount": 1,
                    "OriginalPrice", 110,
                    "ListPrice", 110,
                    "UsedPoint", 10,
                    "BasicPointDiscount", 10,
                    "Subtotal": "90",
                    "TaxType": "Taxable",
                    "ProductType": "Main",
                    "_CustomizedProductId": "X123456",
                    "_ProductName": "\u4fdd\u8b77\u8cbc",
                    "_Spec": "-"
                  }
                ]
              },
              "OrderPackageDate": "2010/11/14",
              "OrderShippingDate": "2010/11/14",
              "_OrderShippingId": "X123456",
              "PickingDate": "2010/11/14",
              "TransferDate": "2010/11/11",
              "_DeliverType": "自行運送(99)",
              "_OrderNote": "請在03/0803/08早上到貨",
              "_OrderStatus": "NEW",
              "_OrderStatusDesc": "未結案"
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
            <SuccessList>
                  <OrderList Count="2">
                        <Order Id="YM1234577">
                              <TransferDate>2010/11/11</TransferDate>
                              <LastShippingDate>2010/11/15</LastShippingDate>
                              <OrderShippingDate>2010/11/14</OrderShippingDate>
                              <OrderCloseDate>2010/11/16</OrderCloseDate>
                              <BuyerConfirmDate>2010/11/15</BuyerConfirmDate>
                              <EntryAccountDate>2010/11/15</EntryAccountDate>
                              <PickingDate>2010/11/14</PickingDate>
                              <OrderPackageDate>2010/11/14</OrderPackageDate>
                              <InvoiceNo>WE92904105</InvoiceNo>
                              <InvoiveDate>2010/11/15</InvoiveDate>
                              <OrderShippingId><![CDATA[X123456]]></OrderShippingId>
                              <DeliverType><![CDATA[自行運送(99)]]></DeliverType>
                              <OrderNote><![CDATA[請在03/0803/08早上到貨]]></OrderNote>
                              <OrderStatus>NEW</OrderStatus>
                              <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
                              <OrderProductList>
                                    <Product Id="p2345677">
                                          <CustomizedProductId><![CDATA[A123456]]></CustomizedProductId>
                                          <ProductType>Main</ProductType>
                                          <ProductName><![CDATA[iphone 4 全配]]></ProductName>
                                          <Spec><![CDATA[黑色]]></Spec>
                                          <Amount>2</Amount>
                                          <OriginalPrice>52000</OriginalPrice>
                                          <ListPrice>52000</ListPrice>
                                          <UsedPoint>0</UsedPoint>
                                          <BasicPointDiscount>0</BasicPointDiscount>
                                          <Subtotal>52000</Subtotal>
                                          <TaxType>Taxable</TaxType>
                                    </Product>
                                    <Product Id="p23456799">
                                          <CustomizedProductId><![CDATA[]]></CustomizedProductId>
                                          <ProductType>Main</ProductType>
                                          <ProductName><![CDATA[iphone 4 皮套]]></ProductName>
                                          <Spec><![CDATA[白色]]></Spec>
                                          <Amount>2</Amount>
                                          <OriginalPrice>0</OriginalPrice>
                                          <ListPrice>0</ListPrice>
                                          <UsedPoint>0</UsedPoint>
                                          <BasicPointDiscount>0</BasicPointDiscount>
                                          <Subtotal>0</Subtotal>
                                          <TaxType>TaxFree</TaxType>
                                    </Product>
                              </OrderProductList>
                        </Order>
                        <Order Id="YM1234588">
                              <TransferDate>2010/11/11</TransferDate>
                              <LastShippingDate>2010/11/15</LastShippingDate>
                              <OrderShippingDate>2010/11/14</OrderShippingDate>
                              <OrderCloseDate>2010/11/16</OrderCloseDate>
                              <BuyerConfirmDate>2010/11/15</BuyerConfirmDate>
                              <EntryAccountDate>2010/11/15</EntryAccountDate>
                              <PickingDate>2010/11/14</PickingDate>
                              <OrderPackageDate>2010/11/14</OrderPackageDate>
                              <InvoiceNo>WE92904106</InvoiceNo>
                              <InvoiveDate>2010/11/15</InvoiveDate>
                              <OrderShippingId><![CDATA[X123456]]></OrderShippingId>
                              <DeliverType><![CDATA[自行運送(99)]]></DeliverType>
                              <OrderNote><![CDATA[請在03/0803/08早上到貨]]></OrderNote>
                              <OrderStatus>NEW</OrderStatus>
                              <OrderStatusDesc><![CDATA[未結案]]></OrderStatusDesc>
                              <OrderProductList>
                                    <Product Id="p2345999">
                                          <CustomizedProductId><![CDATA[X123456]]></CustomizedProductId>
                                          <ProductName><![CDATA[保護貼]]></ProductName>
                                          <ProductType>Main</ProductType>
                                          <Spec><![CDATA[-]]></Spec>
                                          <Amount>1</Amount>
                                          <OriginalPrice>100</OriginalPrice>
                                          <ListPrice>100</ListPrice>
                                          <UsedPoint>10</UsedPoint>
                                          <BasicPointDiscount>10</BasicPointDiscount>
                                          <Subtotal>90</Subtotal>
                                          <TaxType>Taxable</TaxType>
                                    </Product>
                              </OrderProductList>
                        </Order>
                  </OrderList>
            </SuccessList>
            <Receiver>
                  <ReceiverName>
                        <![CDATA[陳美美]]>
                  </ReceiverName>
                  <ReceiverPhone>
                        <![CDATA[02-22222222]]>
                  </ReceiverPhone>
                  <ReceiverMobile>
                        <![CDATA[0911111111]]>
                  </ReceiverMobile>
                  <ReceiverAddress>
                        <![CDATA[台北市士林區文化路1號]]>
                  </ReceiverAddress>
                  <ReceiverZipcode>
                        <![CDATA[100]]>
                  </ReceiverZipcode>
            </Receiver>
      </Transaction>
</Response>
```

### Errors

---

/v1/Order/Cancel
----------------

商店執行取消訂單

### Request parameters

+---------------+------------------+-------------+
| Parameter     | Value            | Description |
+===============+==================+=============+
| TransactionId | string           | 交易序號    |
|               |(Require/15)      |             |
+---------------+------------------+-------------+
| OrderId       | string (Require) | 訂單編號    |
|               |(Require/20)      |             |
+---------------+------------------+-------------+
| CancelRemark  | string (Option)  | 取消備註    |
+---------------+------------------+-------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/Cancel?TransactionId=123456&OrderId=YM1234567890123&Format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/Cancel?TransactionId=123456&OrderId=YM1234567890123&Format=xml
```

請注意： Order API 使用 https 通訊協定。

### Response fields

+----------------+--------------+
| Field          | Description  |
+================+==============+
| OrderCloseDate | 訂單結案日期 |
+----------------+--------------+
| ErrorCode      | 錯誤代碼     |
+----------------+--------------+
| ErrorMessage   | 錯誤訊息     |
+----------------+--------------+

### Sample response

#### JSON sample

```
{
    "Response":
    {
        "@Status":"ok",
        "Transaction":
        {
            "@Id":"123456",
            "Order":
            {
               "@Id":"YM1234567",
               "OrderCloseDate":"2011/11/12"
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
            <OrderCloseDate>2011/11/12</OrderCloseDate>
        </Order>
    </Transaction>
</Response>
```

### Errors

+-----------+--------------------------------------+
| ErrorCode | ErrorMessage                         |
+===========+======================================+
| 2701      | 無法取消訂單：不可單獨取消物流服務費 |
+-----------+--------------------------------------+
| 2702      | 無法取消訂單，請再確認               |
+-----------+--------------------------------------+
| 2703      | 取消物流服務費發生錯誤               |
+-----------+--------------------------------------+
| 2704      | 寄發取消通知信錯誤                   |
+-----------+--------------------------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Order/GetShippingSupplierList
---------------------------------

取得目前設定的貨運商代碼對應表,於出貨確認時使用

### Response fields

+-------+-----------------+
| Field | Description     |
+=======+=================+
| Code  | 貨運商代碼      |
|       |                 |
|       | * 4:新竹        |
|       | * 7:郵局        |
|       | * 9:宅配通      |
|       | * 11:統一宅急便 |
|       | * 12:大榮       |
|       | * 18:便利帶     |
|       | * 99:自行運送   |
+-------+-----------------+
| Name  | 貨運商名稱      |
+-------+-----------------+

Sample Request：

```
https://tw.ews.mall.yahooapis.com/stauth/v1/Order/GetShippingSupplierList?format=xml
                                   OR
https://tw.ews.mall.yahooapis.com/oauth/v1/Order/GetShippingSupplierList?format=xml
```

請注意： Order API 使用 https 通訊協定。

### Sample response

#### JSON sample

```
{
  "Response": {
    "@Status": "ok",
    "ShippingSupplierList": {
      "ShippingSupplier": [
        {
          "@Code": "4",
          "_Name": "\u65b0\u7af9"
        },
        {
          "@ShippingSupplierCode": "7",
          "_Reason": "\u90f5\u5c40"
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
      <ShippingSupplierList>
            <ShippingSupplier Code="4">
                  <Name>
                        <![CDATA[新竹]]>
                  </Name>
            </ShippingSupplier>
            <ShippingSupplier Code="7">
                  <Name>
                        <![CDATA[郵局]]>
                  </Name>
            </ShippingSupplier>
      </ShippingSupplierList>
</Response>
```

### Errors

