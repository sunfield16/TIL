`NSLocale`は主にローカライズで必要な情報を扱うフレームワーク。  
端末上の設定上から、地域や言語設定に基づくデータを取得できる。

## 主に取得できるもの
* 国・地域コード（`FR`や`HK`など）
* 言語コード（`en`や`es`など）
* 通貨コード（`USD`や`JPY`など）
* 通貨記号（`$`や`¥`など）
* 金額の区切り文字（`,`や`.`など、言語ごとに区切り文字が違う）
* 文章上の区切り文字（`"`や`「`など文章上で括る際に使う文字）

## インスタンス
`currentLocale`で現在の設定に基づいたインスタンスを取得できる。
```objC
NSLocale* locale = [NSLocale currentLocale];
```

## データの取得
現在では取得したいデータ別にメソッドが用意されているため、  
それらを使うことで取得可能。

```objC
NSLocale* locale = [NSLocale currentLocale];
NSString* country = [locale countryCode];

// ↓C++と組み合わせて使う場合
std::string country = [[locale countryCode] UTF8String];
```

### `objectForKey`
過去のバージョンではこちらが使われていた。

`objectForKey:`に`NSLocaleKey`を指定することで  
対応するデータを取得できる。
```objC
NSLocale* locale = [NSLocale currentLocale];
NSString* country = [locale objectForKey:NSLocaleCountryCode];
NSString* language = [locale objectForKey:NSLocaleLanguageCode];
```