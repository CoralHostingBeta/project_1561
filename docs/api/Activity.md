/v1/Activity/GetList
--------------------

取得商店的活動列表資料

+-------------+--------------------------------------------------------------+
| Attribute   | Value                                                        |
+=============+==============================================================+
| API Name    | 取得活動列表 (/Activity/GetList)                             |
+-------------+--------------------------------------------------------------+
| API Desc    | 取得活動列表資料                                             |
+-------------+--------------------------------------------------------------+
| Version     | 1                                                            |
+-------------+--------------------------------------------------------------+
| Request URI | https://tw.ews.mall.yahooapis.com/stauth/v1/Activity/GetList |
|             |                      OR                                      |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/Activity/GetList  |
+-------------+--------------------------------------------------------------+
| Change Log  | *                                                            |
+-------------+--------------------------------------------------------------+

### Request parameters

+----------------+------------------+----------------------+
| Parameter      | Value            | Description          |
+================+==================+======================+
| ActivityStatus | string (Require) | 活動進行狀態         |
|                |                  |                      |
|                |                  | * All:全部           |
|                |                  | * NotStart:未開始    |
|                |                  | * OnGoing:進行中     |
|                |                  | * Finished:已結束    |
+----------------+------------------+----------------------+
| ActivityType   | string (Require) | 活動類型             |
|                |                  |                      |
|                |                  | * Promotion:折扣活動 |
|                |                  | * Ecoupon:電子折價券 |
+----------------+------------------+----------------------+
| Position       | Int(Require)     | 由第幾筆開始拿資料   |
+----------------+------------------+----------------------+
| Count          | Int(Require)     | 資料筆數             |
|                |                  |                      |
|                |                  | Count=1~100          |
+----------------+------------------+----------------------+

### Response fields

+-------------------+--------------------------------------------------------------+
| Field             | Description                                                  |
+===================+==============================================================+
| ActivityList      | 包含此商店的活動列表，屬性：                                 |
|                   |                                                              |
|                   | * Count：資料筆數                                            |
|                   | * TotalCount: 符合 ActivityStatus, ActivityType 的總資料筆數 |
+-------------------+--------------------------------------------------------------+
| Activity          | 包含一筆 Activity 的資料，屬性：                             |
|                   |                                                              |
|                   | * Id：折扣活動編號(string)                                   |
+-------------------+--------------------------------------------------------------+
| ActivityType      | 活動類型                                                     |
|                   |                                                              |
|                   | * Promotion:折扣活動                                         |
|                   | * Ecoupon:電子折價券                                         |
+-------------------+--------------------------------------------------------------+
| Title             | 活動名稱 (string)                                            |
+-------------------+--------------------------------------------------------------+
| Description       | 活動說明(string)                                             |
+-------------------+--------------------------------------------------------------+
| SubType           | 折扣子類                                                     |
|                   |                                                              |
|                   | 若ActivityType=ActivityType                                  |
|                   |                                                              |
|                   | * AmountConstrained:滿件型                                   |
|                   | * PriceConstrained:滿額型                                    |
|                   | * SingleReceive:領取型                                       |
+-------------------+--------------------------------------------------------------+
| ActivityStatus    | 活動進行狀態                                                 |
|                   |                                                              |
|                   | * NotStart:未開始                                            |
|                   | * OnGoing:進行中                                             |
|                   | * Finished:已結束                                            |
+-------------------+--------------------------------------------------------------+
| ImageUrl          | 圖片網址                                                     |
+-------------------+--------------------------------------------------------------+
| ActivityUrl       | 活動網址                                                     |
+-------------------+--------------------------------------------------------------+
| ActivityStartTime | 活動開始時間 (timestamp)                                     |
+-------------------+--------------------------------------------------------------+
| ActivityEndTime   | 活動結束時間 (timestamp)                                     |
+-------------------+--------------------------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "ActivityList":{
      "@Count":2,
      "@TotalCount":14,
      "Activity":[
        {
          "@Id":"19708",
          "@ActivityType":"Promotion",
          "_Title":"\u8cb73\u4ef6\u6253\u516b\u6298",
          "_Description":"\u8cb7\u6eff3\u4ef6\u6253\u516b\u6298",
          "ActivityType":"Promotion",
          "SubType":"AmountConstrained",
          "ActivityStatus":"NotStart",
          "_ImageUrl":"http://test.yahoo.com/test.jpg",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/amountPromo?promotion_id=19708&sid=store1",
          "ActivityStartTime":"1327856400",
          "ActivityEndTime":"1327950000"
        },
        {
          "@Id":"19707",
          "@ActivityType":"Promotion",
          "_Title":"\u6eff1000\u9001100",
          "_Description":"\u8cb7\u6eff1000\u9001100,\n\u8cb7\u6eff2000\u5c31\u9001200",
          "ActivityType":"Promotion",
          "SubType":"PriceConstrained",
          "ActivityStatus":"NotStart",
          "_ImageUrl":"",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/pricePromo?promotion_id=19707&sid=store1",
          "ActivityStartTime":"1327510800",
          "ActivityEndTime":"1327600800"
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
        <ActivityList Count="2" TotalCount="14">
            <Activity Id="19708" ActivityType="Promotion">
                <Title>
                    <![CDATA[買3件打八折]]>
                </Title>
                <Description>
                    <![CDATA[買滿3件打八折]]>
                </Description>
                <ActivityType>Promotion</ActivityType>
                <SubType>AmountConstrained</SubType>
                <ActivityStatus>NotStart</ActivityStatus>
                <ImageUrl>
                    <![CDATA[http://test.yahoo.com/test.jpg]]>
                </ImageUrl>
                <ActivityUrl>
                    <![CDATA[http://lu1.yahoo.com/store_admin/view/amountPromo?promotion_id=19708&sid=store1]]>
                </ActivityUrl>
                <ActivityStartTime>1327856400</ActivityStartTime>
                <ActivityEndTime>1327950000</ActivityEndTime>
            </Activity>
            <Activity Id="19707" ActivityType="Promotion">
                <Title>
                    <![CDATA[滿1000送100]]>
                </Title>
                <Description>
                    <![CDATA[買滿1000送100,買滿2000就送200]]>
                </Description>
                <ActivityType>Promotion</ActivityType>
                <SubType>PriceConstrained</SubType>
                <ActivityStatus>NotStart</ActivityStatus>
                <ImageUrl></ImageUrl>
                <ActivityUrl>
                    <![CDATA[http://lu1.yahoo.com/store_admin/view/pricePromo?promotion_id=19707&sid=store1]]>
                </ActivityUrl>
                <ActivityStartTime>1327510800</ActivityStartTime>
                <ActivityEndTime>1327600800</ActivityEndTime>
            </Activity>
        </ActivityList>
    </Response>
```

### Errors

錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Activity/GetPromotion
-------------------------

取得商店的折扣活動細節

+-------------+------------------------------------------------------------------+
| Attribute   | Value                                                            |
+=============+==================================================================+
| API Name    | 取得折扣活動細節 (/Activity/GetPromotion)                        |
+-------------+------------------------------------------------------------------+
| API Desc    | 取得折扣活動細節                                                 |
+-------------+------------------------------------------------------------------+
| Version     | 1                                                                |
+-------------+------------------------------------------------------------------+
| Request URI | http://tw.ews.mall.yahooapis.com/stauth/v1/Activity/GetPromotion |
|             |                          OR                                      |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/Activity/GetPromotion |
+-------------+------------------------------------------------------------------+
| Change Log  | *                                                                |
+-------------+------------------------------------------------------------------+

### Request parameters

+-------------+------------------+-------------------------------------------+
| Parameter   | Value            | Description                               |
+=============+==================+===========================================+
| PromotionId | string (Require) | 折扣活動編號                              |
|             |                  |                                           |
|             |                  | 一次可select多個PromotionId, 最大接受50個 |
|             |                  |                                           |
|             |                  | ex：PromotionId=233&PromotionId=234       |
+-------------+------------------+-------------------------------------------+

### Response fields

+-------------------------+------------------------------------------------+
| Field                   | Description                                    |
+=========================+================================================+
| PromotionList           | 包含Promotion的資料列表，屬性：                |
|                         |                                                |
|                         | * Count：資料筆數                              |
+-------------------------+------------------------------------------------+
| Promotion               | 包含一筆 Promotion 的資料，屬性：              |
|                         |                                                |
|                         | * Id ：折扣活動編號(string)                    |
+-------------------------+------------------------------------------------+
| Title                   | 活動名稱 (string)                              |
+-------------------------+------------------------------------------------+
| Description             | 活動說明(string)                               |
+-------------------------+------------------------------------------------+
| SubType                 | 折扣子類                                       |
|                         |                                                |
|                         | * AmountConstrained:滿件型                     |
|                         | * PriceConstrained:滿額型                      |
+-------------------------+------------------------------------------------+
| ActivityStatus          | 活動進行狀態                                   |
|                         |                                                |
|                         | * NotStart:未開始                              |
|                         | * OnGoing:進行中                               |
|                         | * Finished:已結束                              |
+-------------------------+------------------------------------------------+
| ImageUrl                | 圖片網址                                       |
+-------------------------+------------------------------------------------+
| ActivityUrl             | 活動網址                                       |
+-------------------------+------------------------------------------------+
| ActivityStartTime       | 活動開始時間  (timestamp)                      |
+-------------------------+------------------------------------------------+
| ActivityEndTime         | 活動結束時間  (timestamp)                      |
+-------------------------+------------------------------------------------+
| GroupType               | 活動商品型態                                   |
|                         |                                                |
|                         | * Full:全店商品                                |
|                         | * Partial:部份商品                             |
+-------------------------+------------------------------------------------+
| IsWithPreviousConstrain | 是否與其他優惠合併計算(true/false)             |
+-------------------------+------------------------------------------------+
| AggregateType           | 折扣設定累進計算型態                           |
|                         |                                                |
|                         | * NotAccumulated:單一折扣設定非累進計算        |
|                         | * Accumulated:單一折扣設定累進計算             |
|                         | * Stepped:多折扣設定計算                       |
+-------------------------+------------------------------------------------+
| RuleList                | 折扣設定列表                                   |
+-------------------------+------------------------------------------------+
| Rule                    | 包含一筆折扣設定資訊                           |
+-------------------------+------------------------------------------------+
| PresentType             | 折抵方式                                       |
|                         |                                                |
|                         | 若SubType=AmountConstrained時                  |
|                         |                                                |
|                         | * Money: 買滿Condition件,折Discount元          |
|                         | * FixMoney: 買滿Condition件,只收固定Discount元 |
|                         | * Percentage: 買滿Condition件,折抵Discount%    |
|                         | * Freebie: 買滿Condition件,送贈品FreebieList   |
|                         |                                                |
|                         | 若SubType=PriceConstrained時                   |
|                         |                                                |
|                         | * Money: 買滿Condition元,折Discount元          |
|                         | * Percentage: 買滿Condition元,折抵Discount%    |
|                         | * Freebie: 買滿Condition元,送贈品FreebieList   |
+-------------------------+------------------------------------------------+
| Condition               | 折扣條件 (number/12,2)                         |
+-------------------------+------------------------------------------------+
| Discount                | 折扣數值 (number/12,2)                         |
|                         |                                                |
|                         | 若為贈品則 Discount=0                          |
+-------------------------+------------------------------------------------+
| FreebieList             | 贈品列表，屬性：                               |
|                         |                                                |
|                         | * Count：贈品筆數                              |
+-------------------------+------------------------------------------------+
| Freebie                 | 贈品商品，屬性：                               |
|                         |                                                |
|                         | * Id：商品編號                                 |
+-------------------------+------------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "PromotionList":{
      "@Count":2,
      "Promotion":[
        {
          "@Id":"19709",
          "SubType":"PriceConstrained",
          "_Title":"\u8cb73000\u9001\u8d08\u54c1",
          "_Description":"\u8cb73000\u5c31\u9001\u8d08\u54c1",
          "ActivityStatus":"NotStart",
          "_ImageUrl":"",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/pricePromo?promotion_id=19709&sid=store1",
          "ActivityStartTime":"1327255200",
          "ActivityEndTime":"1327348800",
          "GroupType":"Full",
          "IsWithPreviousConstrain":false,
          "AggregateType":"NotAccumulated",
          "RuleList":{
            "@Count":1,
            "Rule":[
              {
                "PresentType":"Freebie",
                "Condition":3000,
                "Discount":0,
                "FreebieList":{
                  "@Count":1,
                  "Freebie":[
                    {
                      "@Id":"p09491436394"
                    }
                  ]
                }
              }
            ]
          }
        },
        {
          "@Id":"19708",
          "SubType":"AmountConstrained",
          "_Title":"\u8cb73\u4ef6\u6253\u516b\u6298",
          "_Description":"\u8cb7\u6eff3\u4ef6\u6253\u516b\u6298",
          "ActivityStatus":"NotStart",
          "_ImageUrl":"http://test.yahoo.com/test.jpg",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/amountPromo?promotion_id=19708&sid=store1",
          "ActivityStartTime":"1327856400",
          "ActivityEndTime":"1327950000",
          "GroupType":"Full",
          "IsWithPreviousConstrain":true,
          "AggregateType":"NotAccumulated",
          "RuleList":{
            "Rule":[
              {
                "PresentType":"Percentage",
                "Condition":3,
                "Discount":"20.00",
                "FreebieList":{
                  "@Count":0
                }
              }
            ]
          }
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
        <PromotionList Count="2">
            <Promotion Id="19709">
                <SubType>PriceConstrained</SubType>
                <Title>
                    <![CDATA[買3000送贈品]]>
                </Title>
                <Description>
                    <![CDATA[買3000就送贈品]]>
                </Description>
                <ActivityStatus>NotStart</ActivityStatus>
                <ImageUrl>
                    <![CDATA[]]>
                </ImageUrl>
                <ActivityUrl>
                    <![CDATA[http://lu1.yahoo.com/store_admin/view/pricePromo?promotion_id=19709&sid=store1]]>
                </ActivityUrl>
                <ActivityStartTime>1327255200</ActivityStartTime>
                <ActivityEndTime>1327348800</ActivityEndTime>
                <GroupType>Full</GroupType>
                <IsWithPreviousConstrain>false</IsWithPreviousConstrain>
                <AggregateType>NotAccumulated</AggregateType>
                <RuleList Count="1">
                    <Rule>
                        <PresentType>Freebie</PresentType>
                        <Condition>3000</Condition>
                        <Discount>0</Discount>
                        <FreebieList Count="1">
                            <Freebie Id="p09491436394">
                            </Freebie>
                        </FreebieList>
                    </Rule>
                </RuleList>
            </Promotion>
            <Promotion Id="19708">
                <SubType>AmountConstrained</SubType>
                <Title>
                    <![CDATA[買3件打八折]]>
                </Title>
                <Description>
                    <![CDATA[買滿3件打八折]]>
                </Description>
                <ActivityStatus>NotStart</ActivityStatus>
                <ImageUrl>
                    <![CDATA[]]>
                </ImageUrl>
                <ActivityUrl>
                    <![CDATA[http://lu1.yahoo.com/store_admin/view/amountPromo?promotion_id=19708&sid=store1]]>
                </ActivityUrl>
                <ActivityStartTime>1327856400</ActivityStartTime>
                <ActivityEndTime>1327950000</ActivityEndTime>
                <GroupType>Full</GroupType>
                <IsWithPreviousConstrain>true</IsWithPreviousConstrain>
                <AggregateType>NotAccumulated</AggregateType>
                <RuleList>
                    <Rule>
                        <PresentType>Percentage</PresentType>
                        <Condition>3</Condition>
                        <Discount>20.00</Discount>
                        <FreebieList Count="0">
                        </FreebieList>
                    </Rule>
                </RuleList>
            </Promotion>
        </PromotionList>
    </Response>
```

### Errors

+-----------+----------------------+
| ErrorCode | ErrorMessage         |
+===========+======================+
| 3101      | 查無活動資料         |
+-----------+----------------------+
| 3102      | 活動編號數量超過上限 |
+-----------+----------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)

---

/v1/Activity/GetEcoupon
-----------------------

取得商店的折價券活動細節

+-------------+----------------------------------------------------------------+
| Attribute   | Value                                                          |
+=============+================================================================+
| API Name    | 取得電子折價券活動細節 (/Activity/GetEcoupon)                  |
+-------------+----------------------------------------------------------------+
| API Desc    | 取得電子折價券活動細節                                         |
+-------------+----------------------------------------------------------------+
| Version     | 1                                                              |
+-------------+----------------------------------------------------------------+
| Request URI | http://tw.ews.mall.yahooapis.com/stauth/v1/Activity/GetEcoupon |
|             |                        OR                                      |
|             | https://tw.ews.mall.yahooapis.com/oauth/v1/Activity/GetEcoupon |
+-------------+----------------------------------------------------------------+
| Change Log  | *                                                              |
+-------------+----------------------------------------------------------------+

### Request parameters

+-----------+------------------+-----------------------------------------+
| Parameter | Value            | Description                             |
+===========+==================+=========================================+
| EcouponId | string (Require) | 折價券活動編號                          |
|           |                  |                                         |
|           |                  | 一次可select多個EcouponId, 最大接受50個 |
|           |                  |                                         |
|           |                  | ex：EcouponId=233&EcouponId=234         |
+-----------+------------------+-----------------------------------------+

### Response fields

+-------------------+----------------------------------------------------+
| Field             | Description                                        |
+===================+====================================================+
| EcouponList       | 包含Ecoupon的資料列表，屬性：                      |
|                   |                                                    |
|                   | * Count：資料筆數                                  |
+-------------------+----------------------------------------------------+
| Ecoupon           | 包含一筆 Ecoupon 的資料，屬性：                    |
|                   |                                                    |
|                   | * Id：折價券活動編號(string)                       |
+-------------------+----------------------------------------------------+
| Title             | 活動名稱 (string)                                  |
+-------------------+----------------------------------------------------+
| Description       | 活動說明(string)                                   |
+-------------------+----------------------------------------------------+
| SubType           | 折扣子類                                           |
|                   |                                                    |
|                   | * SingleReceive:領取型                             |
|                   | * PriceConstrained:滿額型                          |
+-------------------+----------------------------------------------------+
| IsShowOnStoreHome | 是否在首頁顯示(true/false)                         |
+-------------------+----------------------------------------------------+
| ActivityStatus    | 活動進行狀態                                       |
|                   |                                                    |
|                   | * NotStart:未開始                                  |
|                   | * OnGoing:進行中                                   |
|                   | * Finished:已結束                                  |
+-------------------+----------------------------------------------------+
| Money             | 折價券金額 (number/12,2)                           |
+-------------------+----------------------------------------------------+
| ShoppingPrice     | 買滿幾元 (number/12,2)                             |
|                   |                                                    |
|                   | (若SubType=SingleReceive 則 ShoppingPrice=0)       |
+-------------------+----------------------------------------------------+
| ReceiveMaxCount   | 領取上限數量                                       |
|                   |                                                    |
|                   | (若SubType=PriceConstrained 則  ReceiveMaxCount=0) |
+-------------------+----------------------------------------------------+
| ImageUrl          | 圖片網址                                           |
+-------------------+----------------------------------------------------+
| ActivityUrl       | 活動網址                                           |
+-------------------+----------------------------------------------------+
| ActivityStartTime | 活動開始時間 (timestamp)                           |
+-------------------+----------------------------------------------------+
| ActivityEndTime   | 活動結束時間 (timestamp)                           |
+-------------------+----------------------------------------------------+
| ValidityStartTime | 電子折價券生效時間  (timestamp)                    |
+-------------------+----------------------------------------------------+
| ValidityEndTime   | 電子折價券結束時間  (timestamp)                    |
+-------------------+----------------------------------------------------+

### Sample response

#### JSON sample

```
{
  "Response":{
    "@Status":"ok",
    "EcouponList":{
      "@Count":2,
      "Ecoupon":[
        {
          "@Id":249,
          "_Title":"\u8cb7\u6eff3000\u9001\u6298\u50f9\u5238",
          "_Description":"\u8cb73000\u9001100\u4e0b\u6b21\u7528",
          "SubType":"PriceConstrained",
          "IsShowOnStoreHome":true,
          "ActivityStatus":"NotStart",
          "Money":100,
          "ShoppingPrice":3000,
          "ReceiveMaxCount":0,
          "_ImageUrl":"http://test.yahoo.com/test1.jpg",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/ecouponPromo?promotion_id=249&sid=store1",
          "ActivityStartTime":1327420800,
          "ActivityEndTime":1327593599,
          "ValidityStartTime":1331049600,
          "ValidityEndTime":1331308799
        },
        {
          "@Id":247,
          "_Title":"Title of Ecoupon",
          "_Description":"Description of Ecoupon",
          "SubType":"PriceConstrained",
          "IsShowOnStoreHome":true,
          "ActivityStatus":"OnGoing",
          "Money":100,
          "ShoppingPrice":1000,
          "ReceiveMaxCount":0,
          "_ImageUrl":"",
          "_ActivityUrl":"http://lu1.yahoo.com/store_admin/view/ecouponPromo?promotion_id=247&sid=store1",
          "ActivityStartTime":1320814473,
          "ActivityEndTime":1325998473,
          "ValidityStartTime":1322542473,
          "ValidityEndTime":1324270473
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
        <EcouponList Count="2">
            <Ecoupon Id="249">
                <Title>
                    <![CDATA[買滿3000送折價券]]>
                </Title>
                <Description>
                    <![CDATA[買3000送100下次用]]>
                </Description>
                <SubType>PriceConstrained</SubType>
                <IsShowOnStoreHome>true</IsShowOnStoreHome>
                <ActivityStatus>NotStart</ActivityStatus>
                <Money>100</Money>
                <SubType>PriceConstrained</SubType>
                <SubType>PriceConstrained</SubType>
                <IsShowOnStoreHome>true</IsShowOnStoreHome>
                <ActivityStatus>OnGoing</ActivityStatus>
                <Money>100</Money>
                <ShoppingPrice>1000</ShoppingPrice>
                <ReceiveMaxCount>0</ReceiveMaxCount>
                <ImageUrl>
                </ImageUrl>
                <ActivityUrl>
                    <![CDATA[http://lu1.yahoo.com/store_admin/view/ecouponPromo?promotion_id=247&sid=store1]]>
                </ActivityUrl>
                <ActivityStartTime>1320814473</ActivityStartTime>
                <ActivityEndTime>1325998473</ActivityEndTime>
                <ValidityStartTime>1322542473</ValidityStartTime>
                <ValidityEndTime>1324270473</ValidityEndTime>
            </Ecoupon>
        </EcouponList>
    </Response>
```

### Errors

+-----------+----------------------+
| ErrorCode | ErrorMessage         |
+===========+======================+
| 3101      | 查無活動資料         |
+-----------+----------------------+
| 3102      | 活動編號數量超過上限 |
+-----------+----------------------+

其他錯誤請參閱[共用錯誤表](common_errors.md)
