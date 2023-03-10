## トラック
各テスト内でのテスト設定の単位。  
トラックごとに以下を設定できる。

* テスターのリスト
* apk
* 対象国

## リリース
1つ以上のアプリのバージョンの組み合わせを表す。  
アプリのアップデートをする際に作成が必要。  
（v1.0.0のリリース、v1.0.1のリリースのように分かれるイメージ）

各種テストを行う場合も、それぞれのリリースを作成することになる。  
（クローズドテストの場合はトラック単位でリリースを作成する）

## 内部テスト
最大100人のテスターを登録してテストができる。  
（登録はメールアドレスを指定する）

* クローズドテストやオープンテストよりも早く配信可能
* ライセンステスターに登録されたテスターなら、有料アプリでも無料でDL可能
* 除外対象の端末・配信対象外の国でもDL可能

## クローズドテスト
内部テストよりも広い範囲のテスターに対するテスト。  
トラックを複数作成できる。

機能ごとに開発・デバッグチームが異なる場合などに、各機能ごとのトラックを作成して  
同時並行でデバッグする…といったことが可能。

## オープンテスト
GooglePlayに公開されて、ユーザーの目に見えるテスト。
テスターはストア上からインストールできるし、  
Webサイトやメールでリンクを共有することでもテストに参加させることができる。

## アプリバージョン設定
テスターがアプリをインストールするときは、  
参加しているテストや製品版（本リリース）の中で  
もっともバージョンの高いものがインストールされる。

### 例
バージョンコードが以下のようになっている場合

* 内部テスト ... 10002
* クローズドテスト ... 10003
* オープンテスト ... 10003
* 製品版 ... 10001

このとき、内部テスト対象のテスターは10002のアプリがインストールされる。  
（クローズドテストの対象テスターになっていれば10003になる）

## テストを停止する
各種テストのページから「トラックの一時停止」を行うことで、  
テストの配信を停止することができる。  
一度設定したテストを削除することはできない。

## プロモート（昇格）
内部テスト→クローズテスト→オープンテスト→製品版の順で、  
テストで作成したリリースを昇格させていくことができる。