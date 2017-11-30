使用者認證
==========

使用者需完成認證的申請流程，取得

- StoreAuth 所需的 ApiKey 與 SharedSecret，或
- [OAuth](https://developer.yahoo.com/oauth2/guide/) 所需的 ClientId 與 Access Token。

申請流程
--------

### OAuth

1. 請先至 developer.yahoo.com [開啟專案](https://developer.yahoo.com/apps/create/)，取得一組 Consumer Key 及 Consumer Secret 後
2. 您將需要使用該組 Consumer Key (又名 ClientId) 徵詢使用者的授權
3. 使用者同意授權後，您將透過 callback 的方式收到可使用的 Access Token

詳細流程請參閱 [OAuth - Explicit Grant Flow](https://developer.yahoo.com/oauth2/guide/flows_authcode/)

### StoreAuth

1. 請向您的超級商城業務窗口提出使用 API 的申請
2. 經過業務窗口初步審合使用資格後
3. 您將需要簽署 API 使用同意書，確保您了解並會妥善保管您所取得的 ApiKey 與 SharedSecret。
4. 您將透過 e-mail 收到您的商店可以使用的 ApiKey 與 SharedSecret

以下為申請流程的簡單說明圖：

![申請流程](images/auth_apply.png)

認證方式
========

### 何謂認證

認證是對於發送 request 的一方的身份識別及檢核的一段處理程序。

透過認證的處理程序讓接收與發送request的雙方可以基於信任的基礎，讓應該受到保護的資料可以被存取，因此請妥善保管。

- OAuth 的憑證為 Access Token + StoreId
- StoreAuth 的憑證為 ApiKey + SharedSecret，以下的章節將分別在介紹 ApiKey 及 SharedSecret。

以下為認證流程的簡單說明圖：

![認證流程](images/auth_process.png)

## 認證流程

當你使用SuperMall提供的API時，請依據使用的 auth method 準備好以下的資料讓你的request可以完成認證：

### OAuth

AccessToken
: AccessToken是一組有時效性的序號。時效過後，需再使用 RefreshToken 換取新的 AccessToken。OAuth 將以 AccessToken 確認您可存取的功能及授權的使用者資訊。

: 長度: 180 bytes

: 格式如下: `ZGoweUptazlhazVJWjJ4NVdtTnNhSHA2Sm1ROVdWZHJPVk5xUWtKVU1uUllUakpyYldOSGJ6bE5RUzB0Sm5NOVkyOXVjM1Z0WlhKelpXTnlaWFFtZUQxaFlRLS06NmYzYjI5NjllYzUwOTkxNDM4MDdiNDU4ZTU5MTc5MzFmYmEzMWUwOA==`

StoreId
: StoreId 為您要存取的店家代號

: 長度: 32 bytes

: 格式如下: `abcd`

Request 傳送方法如下

      GET https://tw.ews.mall.yahoapis.com/oauth/{Version}/{Group}/{Action}?StoreId=abcd&Format=xml
      Authorization: Bearer ZGoweUptazlhazVJWjJ4NVdtTnNhSHA2Sm1ROVdWZHJPVk5xUWtKVU1uUllUakpyYldOSGJ6bE5RUzB0Sm5NOVkyOXVjM1Z0WlhKelpXTnlaWFFtZUQxaFlRLS06NmYzYjI5NjllYzUwOTkxNDM4MDdiNDU4ZTU5MTc5MzFmYmEzMWUwOA==

### StoreAuth

ApiKey
: ApiKey是一組具有唯一識別性的代號，StoreAuth可以透過你的ApiKey取得你的SharedSecret。請妥善保管您的ApiKey，他將會是StoreAuth對您的商店的唯一識別碼。

: 長度: 32 bytes

: 格式如下: `8b337636394c4a9d24292ca20fe06b66`

Signature
: 每一個request都必須包含一組可以被驗證的request sign，否則request將會被拒絕。request signature需要利用你的SharedSecret來計算過，所以請妥善保管你的SharedSecret，應該只有你與StoreAuth知道這一組SharedSecret。

: 長度: 44 bytes

: 格式如下: `O07WYrbfP1CgdtWRFzuuFELE_QmZ6nGp7QC_yjeIGnM-`

Date
: 每一個request都必須包含這個request的time stamp。

以下我們假設您已經取得了ApiKey與SharedSecret，當您要對SuperMall提供的API發送request時，都必須透過StoreAuth才可執行。以下說明圖將對發送request端與StoreAuth與SuperMall API間的流程做個簡單的說明：

![認證流程](images/auth_flow.png)

## 如何製作簽章

Step 1

![](images/MakeSignature1.png)

Step2

![](images/MakeSignature2.png)

*ApiKey*

      8b337636394c4a9d24292ca20fe06b66

*Shared Secret*

      O07WYrbfP1CgdtWRFzuuFELE_QmZ6nGp7QC_yjeIGnM-

*TimeStamp*

      1256489417

*Query String(call API 傳入之參數)*

      Id=23336&Name=中文&Format=xml

*Request Content = API Key+TimeStamp+Query String*

      ApiKey=8b337636394c4a9d24292ca20fe06b66&TimeStamp=1256489417&Id=23336&Name=中文&Format=xml

*Signature = HMacSHA1(RequestContent, Secret)*

      2f03ce8618c5d201314e11f1a3f0fb62e553620f

將以上資料含Signature 送至Server，整包Request 的內容如下

      ApiKey=8b337636394c4a9d24292ca20fe06b66&TimeStamp=1256489417&Id=23336&Name=%E4%B8%AD%E6%96%87&Format=xml&Signature=2f03ce8618c5d201314e11f1a3f0fb62e553620f

## 錯誤代碼

 | ErrorCode | ErrorMessage                                             |
 |-----------|----------------------------------------------------------|
 | 20        | 沒有傳入Format 參數(Format=xml or Format=json)           |
 | 99        | 系統內部錯誤，請稍後再試                                 |
 | 101       | 驗證資訊不足(請檢查ApiKey/TimeStamp/Signature是否有傳入) |
 | 102       | TimeStamp已經失效                                        |
 | 103       | 不合法的使用者(請確定是否已經申請ApiKey and Secret)      |
 | 104       | 簽章驗証失敗                                             |


