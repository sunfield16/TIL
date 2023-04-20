アクセス許可（Permissions）は、アプリが[GraphAPI](/Facebook/GraphAPI.md)で  
データにアクセスするための認証形態。

アプリでFacebookSDKを使用するにあたって、扱うデータに応じて  
必要なアクセス許可を付与する必要がある。

アクセス許可には以下のようなものがある。

* `user_birthday` ... ユーザーの誕生日設定を取得する
* `user_friends` ... ユーザーのフレンドで、そのアプリを利用している人を取得する
* `user_posts` ... ユーザーのタイムライン投稿一覧を取得する

## アプリレビュー
一部を除き、アクセス許可を付与する場合には  
Facebookの[アプリレビュー](/Facebook/Developer/AppReview.md)を申請しなければならない。

不要なアクセス許可を付与しようとしたりすると、申請が通らない原因になる。

### アプリレビューなしで使用可能なもの
以下のアクセス許可はアプリレビューをしなくても使用可能。

* `email` ... ユーザーのメールアドレスを取得する
* `public_profile` ... デフォルトで公開されている情報を取得する
  - ユーザーのID・名前・プロフィール画像など