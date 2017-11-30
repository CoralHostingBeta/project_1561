URI
===

URI採用以下的格式： `https://tw.ews.mall.yahoapis.com/{Auth}/{Version}/{Group}/{Action}`

Auth
: Auth Method (stauth/oauth)

Version
: API Version (v1/v2/v3)

Group
: API Group (Product/MallCategory)

Action
: API Action (Get/GetDetail)

Example: `https://tw.ews.mall.yahooapis.com/stauth/v1/MallCategory/Get`

Request format
==============

Request 使用 REST format。

REST 是使用的最簡單的要求格式 - 它是簡單的 HTTP GET 或 POST 動作。

 * Format 為必要的參數，接受 `"xml"`, `"json"` 二種格式的輸出

Response format
===============

Response 提供 JSON、XML format

JSON
----

JSON (JavaScript Object Notation) 是一種簡單的電腦可讀取資料交換格式，它使得在 JavaScript 中構建 API 應用程式變得更容易。如需有關 JSON 的更多資訊，請見 [json.org](http://www.json.org/)。

若要以 JSON 格式傳回 API response，請在request中的Format參數中帶入JSON。

### Example

`https://tw.ews.mall.yahooapis.com/stauth/v1/MallCategory/Get?Format=json`

### Success response

```js
{
  "Response": {    
    "@Status": "ok",     
    // [payload here]
  }
}
```

### Failure response

```js
{  
  "Response": {    
    "@Status": "fail",     
    // [payload here]
  }
}
```

XML
---

若要以XML格式傳回 API response，請在 request 中的 Format 參數中帶入 XML。若 Format 若無傳入，則 default 為 XML 輸出。

### Example

`https://tw.ews.mall.yahooapis.com/stauth/v1/MallCategory/Get?Format=xml`

### Success response

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
  <!-- [payload here] -->
</Response>
```

### Failure response

```
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="fail">
  <!-- [payload here] -->
</Response>
```
