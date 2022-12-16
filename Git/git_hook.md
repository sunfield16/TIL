## git hook
`git hook`は、gitのcommitやpushなど  
各種動作をトリガーにして処理を行える機能。

* commit前にLinterを実行してコードを整形
* リモートリポジトリにpushがあった場合に自動でpullを行う

など、活用方法は多岐にわたる。

## hookの種類
クライアントサイドフックとサーバーサイドフックがある。
それぞれのタイミングに自動実行される。

### クライアントサイドフック
クライアントのリポジトリ（基本的にはローカルPCの開発環境）  
に配置しておくことで使用可能。

* pre-commit
* prepare-commit-msg
* post-commit
* applypatch-msg
* pre-applypatch
* post-applypatch
* pre-rebase
* post-rewrite
* post-checkout
* post-merge
* pre-push

### サーバーサイドフック
リモートリポジトリに配置することで使用可能。  
デプロイ先のリポジトリではなく、**リモートリポジトリ**に配置する必要がある。

* pre-receive
* update
* post-receive

## フックを配置する
gitリポジトリを作成すると、以下の場所にフック配置用のディレクトリが作成される。  
サンプルも配置されているので、動作確認の際に活用可能。

```
[リポジトリのルート]/.git/hooks/
  - applypatch-msg.sample
  - commit-msg.sample
  - fsmonitor-watchman.sample
  - post-update.sample
  - pre-applypatch.sample
...
```

この`hooks`ディレクトリに、フック名のファイルを配置することで  
各タイミングに自動実行されるようになる。
（サンプルには`.sample`がついているが、これも削除する必要あり）

また、実行権限を付与する必要がある。

```bash
# commit-msgを使用する際の例
# 名前の.sampleを削除
mv commit-msg.sample commit-msg

# 実行権限を付与
chmod +x commit-msg
```