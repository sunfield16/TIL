[[htaccess|.htaccess]]でBasic認証を導入する時に設置が必要なファイル。    
ここに書かれているIDとパスワードを入力することでアクセスができるようになる。

以下のようにIDとパスワードを並べて記載するが、パスワードは暗号化が必要。
```
id:password
id:password
id:password
...
```

## `.htpasswd`の作成
<https://analyzegear.co.jp/blog/1881>

生成するWebサービスがいくつかあるほか、  
`htpasswd`コマンドで作成できる。（Macにもある）
```bash
# -c で新しいファイルを作成、オプション指定しない場合は追記
htpasswd -c ./.htpasswd [ユーザー名]

# 実行するとパスワードを聞かれるので入力（2回やる）
New password: 
Re-type new password:
```