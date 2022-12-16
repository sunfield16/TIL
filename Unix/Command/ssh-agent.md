## ssh-agent
`ssh-agent`は、RSAなどの公開鍵認証で使う秘密鍵を保持する際に使われるプロセス。

プロセス起動後に秘密鍵を登録しておくことで、  
ssh接続などの際に鍵ファイルの指定やパスフレーズ入力をスキップできる。

## ssh-add
`ssh-agent`に秘密鍵を登録する際に使用するコマンド。  
登録解除もこれで行う。

## 基本の使用方法
### ssh-agent
```bash
$ ssh-agent [オプション]
```

### ssh-add
```bash
ssh-add [オプション] [秘密鍵のパス]
```

## ssh-agentの起動
オプションなしで実行することで起動可能。  
ただし、基本的には`eval`と組み合わせる形で実行する。
```bash
$ eval "$(ssh-agent)"
```

ssh-agentは以下のようにシェルで設定する用の環境変数が出力されるようになっていて、  
`eval`と組み合わせることで即座に変数を設定している。
```bash
$ ssh-agent

SSH_AUTH_SOCK=/var/folders/rx/2t209yf11n5bcr91hhltvn280000gn/T//ssh-wKdXTNGmv2wX/agent.4864; export SSH_AUTH_SOCK;
SSH_AGENT_PID=4864; export SSH_AGENT_PID;
echo Agent pid 4864;
```

## 秘密鍵を登録・解除する
ssh-agentを起動したら、ssh-addを実行して秘密鍵を登録できるようになる。
```bash
$ ssh-add /path/to/ssh/hogehoge.id_rsa
Enter passphrase for /path/to/ssh/hogehoge.id_rsa: 
Identity added: /path/to/ssh/hogehoge.id_rsa (/path/to/ssh/hogehoge.id_rsa)
```

登録解除は`-d`や`-D`で行う。
```bash
# -d で単体解除、 -D で全部解除
$ ssh-add -d /path/to/ssh/hogehoge.id_rsa
$ ssh-add -D
```

登録した鍵は`-l`で確認できる。
```bash
$ ssh-add -l
2048 SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx /path/to/ssh/hogehoge.id_rsa (RSA)
```

## ssh-agentプロセスを閉じる
`-k`を指定すると、プロセスを閉じるための出力がされる。
```bash
$ ssh-agent -k

# 出力
unset SSH_AUTH_SOCK;
unset SSH_AGENT_PID;
echo Agent pid 4864 killed;
```
プロセス開始時と同じく`eval`を組み合わせることで、プロセスを閉じることが可能。
```bash
$ eval "$(ssh-agent -k)"
```

## シェルスクリプト上で使う
シェルスクリプト上だけの限定で利用する場合は、  
スクリプトの最初でプロセスを起動し、最後に閉じる形で限定的な使用ができる。

（途中の強制終了に対応する場合は、`trap`などの例外処理で対処が必要になる）
```bash
#!/bin/bash
$ eval "$(ssh-agent)"

~~~色々な処理を実行~~~

$ eval "$(ssh-agent -k)"
```