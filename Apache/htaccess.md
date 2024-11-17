https://httpd.apache.org/docs/2.4/ja/howto/htaccess.html  
https://qiita.com/sanogemaru/items/7e5bd6e8dc9b04c9978e  
https://www.kagoya.jp/howto/it-glossary/web/htaccess/

[[Apache]]の環境で使用可能な、サーバー設定用のファイル。  
（ファイル名は`.htaccess`のように頭に`.`をつける）

ディレクトリ単位で以下のような設定を行うことができる。  

* Basic認証
* リダイレクトの設定
  - Webページを移転する時
* アクセスできるIPやドメインの制限
* ファイル一覧表示の禁止

設定した内容は設置した場所から直下のディレクトリに適用される。

ただし、基本的にはこれを使わないことが推奨されている。  
`httpd.conf`で同じ設定ができるため、これでサーバー全体に設定する方がよい。

`.htaccess`は「root権限はないけどディレクトリごとの設定をしたい」時などに使う。  
（状況としてはレンタルサーバーなど）