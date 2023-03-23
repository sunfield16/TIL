ProtocolBuffersは、データのシリアライズを行う  
言語・プラットフォームに依存しないライブラリ。

オープンソースとしてGitHubにも公開されている。

## 特徴
* JSONよりも小サイズで高速
* C++, C#, Java, Pythonなど様々な言語に対応
* gRPCで利用できる
* 小さいデータを扱うのに向いている
  - 1MBを超えるようなデータは苦手

## インストール
homebrewからインストール可能。  
ただし、各言語で使用する際には別途でパッケージのインストールが必要になる。
```bash
brew install protobuf
```

## スキーマの作成
ProtocolBuffersを使用する際は、シリアライズしたいデータの構造（`.proto`）を定義する。

```proto
/* バージョン指定（基本はproto3） */
syntax = "proto3";

package foo.bar;

/* メッセージ「MyMessage」を作成
 * これが1つのデータ構造になる */
message MyMessage 
{
	/* 各データにはそれぞれを識別するためのタグを設定する（重複不可） */
    int32 id = 1;
    string name = 2;
    string description = 3;
}
```

その後、`protoc`を実行することで  
そのデータ構造を各言語で使うためのクラス設計などを自動生成できる。
```bash
# 例: Python用のクラスを作成する場合
protoc --proto_path=[.protoファイルのディレクトリ] --python_out=[クラスの生成場所] [.protoファイル]
```