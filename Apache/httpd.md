## httpd
httpdはHTTPによるデータ転送を扱うデーモン。  
主にWebサーバーでHTTPのリクエストを処理する際に活躍する。

Apacheに限らず、他のWebサーバーソフトウェアでも利用される。

## httpd.conf
httpdに関する様々な設定は`httpd.conf`に記述する。  
起動（再起動）時のみ読み込まれるため、設定を調整してもすぐに反映されるわけではない。

## 基本構文
```
# "#"で始まる行はコメント
# 設定のある行の末尾にコメントはつけられない

# 基本は[項目] [設定値]で設定
ServerName www.example.com:80

# <>でブロックを指定できる
<Directory />
    AllowOverride none
    Require all denied
</Directory>
```

構文チェックはコマンドによって行える。
```bash
apachectl configtest
```

## Include
`Include`によって、他の設定ファイルの内容を読み込むことができる。  
ワイルドカード等で一度に複数に読み込みも可能。

```
# 単体
Include /usr/local/apache2/conf/ssl.conf

# 複数同時読み込み
Include /usr/local/apache2/conf/vhosts/*.conf
```