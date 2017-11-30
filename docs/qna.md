Q ＆ A
-------
# 簽章(Signature)相關
--------------------
Q》使用者認證方式？
: A》我們稱為StoreAuth, 就是以商店為單位的認證方式，StoreAuth 的憑證為 ApiKey + SharedSecret，利用ApiKey+SharedScret再製作出簽章(Signature)

Q》Time Stamp效期？每次都要重傳嗎？
: A》Time Stamp效期1次1分鐘，每次都要重傳才能確認店家身份而不致被其他駭客盗取資料

Q》哪些資料需做簽章？
: A》需要將所有Request的參數都要做Signature，之後將所有Signature之結果＋Signature一起傳出

Q》產生之signature放置的位置
: A》做signature時請先不要URLencode（包含中文), 做出來的signature需加在POST body的最後

# 商品(Product)相關
-------------------
Q》系統自動下架商品時機？
: A》1.商品0庫存，12~15天後系統會自動下架; 2.商品更新時的SalePrice與原本的SalePrice不同時系統自動下架



