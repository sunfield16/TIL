Node.js向けに作成されたWebフレームワークの1つ。

* 基礎的なWebアプリケーション向けの機能を提供
* 堅牢なAPIをシンプルに素早く作成できる

などが謳われている。

## インストール
```bash
npm install express
```

## サーバーを起動する
`express()`で取得したオブジェクトのメソッドを使うのが基本になる。

`listen(port, function)`でExpressサーバーを起動。  
指定したポートへのアクセスを受け付ける。

functionは起動時のコールバック。
```javascript
const express = require('express');
const app = express();

// アクセス受付
const server = app.listen(3000, function(){
  console.log("server start: " + server.address().port);
});
```