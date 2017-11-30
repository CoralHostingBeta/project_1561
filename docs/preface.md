概要
====

超級商城提供API給，於超級商城開立網路商店的店家，可透過API新增/修改/取得商店的資料。

將提供兩種使用者認證方式，StoreAuth與OAuth。

目前僅提供StoreAuth的認證方式，供內部有技術人員，使用ERP且於超級商城刊登大量商品資料的店家使用。

預計於2010年提供OAuth的認證方式，供內部有技術人員且於超級商城刊登大量商品資料的店家使用。第三方技術廠商亦可申請使用此認證方式開發超級商城使用者端工具，超級商城店家使用。

使用API時，請依據此文件中的Request format傳送所需的參數至指定的API，將會收到一組格式化的回覆。

使用前必讀
----------

### 權利與義務

取得 API Key 及 Shared Secret 即可使用商城API，請妥善保管API Key 及 Shared Secret。如發現不當使用，站方可依狀況終止使用權利。

### API Key and Shared Secret

API Key 及 Shared Secret 如同存取超級商城的使用者帳號及密碼，請妥善保管。請勿將此資訊散布至個人電腦中，造成API Key and Shared Secret失竊的風險。

### TimeStamp

TimeStamp 為 Unix Timestamp，格式如下: `1256483643`，由1970年1月1日 UTC 時間開始計算，每經過一秒，數字就會加一。每一個 Request 都必須帶著 TimeStamp，請使用 [/echo API](api/echo.md) 來取得現在系統時間。

編碼
----

超級商城所有資料使用 **UTF-8** 編碼。
