/echo
=====

此為取得伺服器時間，以調整 API 送出之 TimeStamp 值。

*此API 不需要經過驗証簽章*

Sample Request: `https://tw.ews.mall.yahooapis.com/stauth/v1/echo?Format=xml`

### Response fields

| Field         | Description    |
|---------------|----------------|
| TimeStamp     | Unix TimeStamp |
| LocalDateTime | 當地時間       |
| UTCDateTime   | UTC 標準時間   |

### Sample response

#### JSON sample

```js
{
  "Response":{
    "TimeStamp":1256482384,
    "LocalDateTime":"2009-10-25T22:53:04+0800",
    "UTCDateTime":"2009-10-25T14:53:04Z",
    "@Status":"ok"
  }
}
```

#### XML sample

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response Status="ok">
  <TimeStamp>1256481454</TimeStamp>
  <LocalDateTime>2009-10-25T22:37:34+0800</LocalDateTime>
  <UTCDateTime>2009-10-25T14:37:34Z</UTCDateTime>
</Response>
```

 | ErrorCode | ErrorMessage |
 |-----------|--------------|
 |           |              |
