`Secure Copy`の略で、sshを使ってリモートマシンにファイルを転送するコマンド。  
scpは正確にはプロトコルの1つ。

現在は非推奨であるともされており、rsyncや[sftp](/Unix/Command/sftp.md)などへ置き換えるべきとの話もある。  
RedHatでは非推奨になっている模様。  
https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/9/html/9.2_release_notes/deprecated-functionality-security

## 基本の使い方
```bash
scp [オプション] [コピー元パス] [保存先パス]
```

### 例
* 転送するもの　: `hogehoge.zip`
* コピーする場所: 接続先`fugafuga@000.000.000.000`の`/path/to/dst/`

といった場合、以下のようになる。
```bash
scp "hogehoge.zip" "fugafuga@000.000.000.000:/path/to/dst/"
```

## 参考
https://ja.wikipedia.org/wiki/Secure_copy  
https://qiita.com/chihiro/items/142ebe6980a498b5d4a7  
https://qiita.com/tomoyk/items/bf18eec969486b6fc3c4