## オプション（構成）ファイル
MySQLでは、起動時に規定のファイルから各種オプション設定を読み取ることができる。  
普通、オプション設定はMySQLの起動ごとにコマンドで設定しなければならないが、  
規定のファイルに記載しておけばそれらを勝手に設定してくれる。

## オプションファイルの配置・読み取り
Linuxに関しては、下記の場所に配置してあるファイルが起動時に読み取られる。

ファイル名             | 目的
---------------------|----------------
/etc/my.cnf          | グローバルオプション
/etc/mysql/my.cnf    | グローバルオプション
SYSCONFDIR/my.cnf    | グローバルオプション
${MYSQL_HOME}/my.cnf | サーバー固有のオプション
defaults-extra-file  | `--defaults-extra-file=path` によって指定されるファイル (ある場合)
${HOME}/.my.cnf      | ユーザー固有のオプション
${HOME}/.mylogin.cnf | ログインパスオプション


## 設定方法
`ini`の形式で記載する。

### 設定例
[公式サイト](<https://dev.mysql.com/doc/refman/5.6/ja/option-files.html)に>  
上がっている例を記載する。

```ini
[client]
port=3306
socket=/tmp/mysql.sock

[mysqld]
port=3306
socket=/tmp/mysql.sock
key_buffer_size=16M
max_allowed_packet=8M

[mysqldump]
quick
```

### セクション
`[]`で、設定のグループである「セクション」を指定する。  
セクションごとに設定できる内容が異なるので注意が必要。

* `[client]`
  - MySQLクライアントを起動時に設定するもの
  - mysqlコマンドでMySQLに接続する時に使われる
  - なので、WebサーバーからMySQL用サーバーに接続する場合にはWebサーバー側に設定が必要
* `[mysqld]`
  - MySQLサーバーに保存されているシステム変数
* `[mysqld_safe]`
  - MySQLサーバーを起動する時の設定
* `[mysqldump]`
  - mysqldump向けの設定