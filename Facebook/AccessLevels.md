アクセスレベル（AccessLevels）は、アプリの[[Permissions|アクセス許可]]と[[Features|機能]]に対して  
適用されるレイヤー。  
[[AppType]]が`Consumer`,`Business`,`Gaming`のアプリにのみ存在する。

## 種類
アクセスレベルには2種類ある。

* `Standard`（標準アクセス）
* `Advanced`（高度なアクセス）

### Standard
主にロールを持つユーザーのみが使う想定のアプリや、アプリの開発中に  
APIエンドポイントへのアクセスをテストする時に使う。

[[Permissions|アクセス許可]]の場合はそのアプリに対してロールを持つユーザーのみ要求できる。  
[[Features|機能]]の場合はそのアプリに対してロールを持つユーザーのみ有効になる。

`Consumer`,`Business`,`Gaming`のアプリは、利用可能なアクセス許可と機能の  
アクセスレベルはデフォルトで全て`Standard`になる。

### Advanced
全てのユーザーに対して有効になる。
アクセス許可や機能の種類によっては[[AppReview|アプリレビュー]]が必要になることもある。

また、2023/05/01以降から、このアクセスレベルを使う場合には  
[[Business|ビジネス認証]]が必要になる模様。

## 参考
https://developers.facebook.com/docs/graph-api/overview/access-levels  
https://developers.facebook.com/docs/development/release/business-verification