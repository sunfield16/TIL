## 参考資料
<https://dev.mysql.com/doc/refman/5.6/ja/time-zone-support.html>

<https://unrealman.hatenablog.com/entry/mysql-timezone>

## MySQLのタイムゾーン設定
MySQLには3つのタイムゾーン設定がある。

* ホストのタイムゾーン設定
  - MySQL起動時に、ホストの設定を読み取って`system_time_zone`システム変数に入れる
* MySQLセッション設定
  - その接続の間のみ適用される`time_zone`システム変数
* MySQLグローバル設定
  - 現在サーバーに設定されている`time_zone`システム変数

## タイムゾーンが影響するもの
* `NOW()` や `CURTIME()`などの関数
* `TIMESTAMP`カラムに保存される値
  - 保存時に現在のタイムゾーン → UTCに変換される
  - 取得時はUTC → 現在のタイムゾーンに変換される

## タイムゾーンが影響しないもの
* `UTC_TIMESTAMP()` 関数
* `DATE`, `TIME`, `DATETIME`カラムに保存される値

## `system_time_zone`
MySQLが入っているサーバーのタイムゾーン設定が入る。  
例えばUTCになっていた場合は以下のようになる。
```
system_time_zone="UTC"
```

## `time_zone` 
最終的にはこのシステム変数によって決まる。  
設定できるのは以下の通り。

* 各種タイムゾーン ... JST, UTCなど。大文字・小文字の区別はない
* SYSTEM ... `system_time_zone`の設定を参照する
* UTC±指定 ... `+10:00`や`-6:00`など、UTCからの時差を指定する