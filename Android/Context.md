Contextはアプリケーションのリソースや各種グローバル情報にアクセスするためのクラス。  
ActivityやApplicationクラスはこれを継承している。

* アプリケーションのリソースへのアクセス
* 各種グローバル情報の取得
* アプリケーションレベルでの操作
  - アクティビティやサービスの起動
  - Intentの作成

などで必要になり、Androidアプリ開発においては各所で使用される。

## Contextの種類
* `Activity Context`
* `Application Context`

### `Activity Context`
アクティビティのライフサイクルに依存したContext。  
アクティビティが破棄されるタイミングで同時に破棄される。

アクティビティの`this`によって参照できる。
（アクティビティそのものがContextを継承しているため）

### `Application Context`
アプリケーション全体に関わるContext。　　
アプリ全体のライフサイクルで使用したい場合はこちらを使う。

アクティビティなどの`getApplicationContext()`で参照できる。

## 参考
https://developer.android.com/reference/android/content/Context  
https://qiita.com/tkmd35/items/e6abeed6ac68cbac09ed  
https://zenn.dev/issyu_39/articles/5225144dae22efc162fd