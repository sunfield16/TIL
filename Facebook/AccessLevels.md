アクセスレベル（AccessLevels）は、アプリの[アクセス許可](/Facebook/Permissions.md)と[機能](/Facebook/Features.md)に対して  
適用されるレイヤー。  
[AppType](/Facebook/Developer/AppType.md)が`Consumer`,`Business`,`Gaming`のアプリにのみ存在する。

## 種類
アクセスレベルには2種類ある。

* `Standard`（標準アクセス）
* `Advanced`（高度なアクセス）

### Standard
主にロールを持つユーザーのみが使う想定のアプリや、アプリの開発中に  
APIエンドポイントへのアクセスをテストする時に使う。

[アクセス許可](/Facebook/Permissions.md)の場合はそのアプリに対してロールを持つユーザーのみ要求できる。  
[機能](/Facebook/Features.md)の場合はそのアプリに対してロールを持つユーザーのみ有効になる。

`Consumer`,`Business`,`Gaming`のアプリは、利用可能なアクセス許可と機能の  
アクセスレベルはデフォルトで全て`Standard`になる。

### Advanced
全てのユーザーに対して有効になる。
アクセス許可や機能の種類によっては[アプリレビュー](/Facebook/Developer/AppReview.md)が必要になることもある。