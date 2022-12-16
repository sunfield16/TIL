# Jenkinsをはじめる
## 参考資料
[Jenkins を Mac にインストールして LAN内の PC から接続するまで](https://qiita.com/enuesutea/items/45527625362e5f3cc17b)

## Jenkinsとは
Jenkinsは、最近よく聞く「**CI/CD**」を支援するソフト。

* 日頃から行ってる単純な作業があるが、手順確認しながらやったりでめんどくさい
  - しかも手順間違えたり抜けたりして失敗する可能性がある
* 毎日定時前にアプリをビルドして帰るけど、いちいちビルド実行するのがだるい
  - 忘れる可能性あるし定時前だし…
* 作業用のPCを共有して使う場合に作業中の人がいるかを毎回確認しなくちゃいけない

こういった「単純作業」や「継続的に行うこと」を自動でやってもらえるようにするためのツールが「Jenkins」である。

基本的には、「継続的な、開発からビルド→リリース」のような開発の単純作業を自動的に行い、作業の効率化を図る目的で使われる。  

## Jenkinsで自動化するのに向いてること
* 単純だけどやる頻度が多い作業
* 手順が多いけどやること自体は毎回同じな作業
* 毎日決まった時間に行う作業

## Jenkinsで自動化するのに向いてないこと
* 状況に応じて毎回やることが違う作業
* 機械では判定できず、確認に人の手が必要になる作業


## インストール
`homebrew`を使うことで簡単にインストールできる。

``` bash
brew install jenkins
```

ただしJenkinsの実行には`JDK`が必要になるため、こちらもインストールしておくこと。  
※今回はインストール確認で使ったPCにJDKが入っていたが、入っていなかった場合の導入方法も後に記載したい

## 起動
起動する場合のコマンドも単純。

``` bash
# Jenkins、起動！
jenkins
```

実行すると起動ログが流れてくる。

## Jenkinsにアクセスしてみる
流れる起動ログの中に、下記のようなログが発見されたらJenkinsが起動された合図。  
（ログ自体は流れているが、この時点で起動はしている）

``` bash
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

abcdefghijklmnopqrstuvwxyz012345

This may also be found at: /Users/hoge/.jenkins/secrets/initialAdminPassword
```

これが出たら「`localhost:8080`」にブラウザで接続すると、Jenkinsの初期設定画面に飛んでくれる。  
上のログで表示されている文字列が「管理者のパスワード」になっているので、これを入力して管理者としてログインができる。

## バックグラウンドで起動
jenkinsは無事起動できたが、これだと実行しているターミナルを閉じたりした場合にjenkinsが終了してしまう。  
そのため基本的にはバックグラウンドで実行することになる。

homebrewの機能を使うことで簡単に起動・停止が可能。

``` bash
# バックグラウンドで起動
brew services start jenkins

# 停止
brew services stop jenkins

# 再起動
brew services restart jenkins
```