## FlatBuffers
FlatBuffersはデータのシリアル化を行うクロスプラットフォームのライブラリ。  
元々はゲーム等の高パフォーマンスが求められるアプリのために、Google内で作成された。

オープンソースとしてGitHubにも公開されている。

## 特徴
* C++、C#、Java、Javascript、Python、PHPなど様々な言語で使用可能
* JSONや他のシリアル化ライブラリに比べて高速で、メモリの消費も抑えられる
  - ベンチマークについては公式サイトでも公開されている

## インストール
MacであればHomebrewで簡単に導入できる。

```bash
$ brew install flatbuffers
```

## fbsからデータ構造を各言語用にコンパイルする
flatbuffersのコマンドを使って、作成したfbsから  
各言語で使えるデータ構造を生成する。

```bash
# 例1:PHPの場合
flatc --php hogehoge.fbs

# 例2:Pythonの場合
flatc --python hogehoge.fbs
```

実際のソースコードでは、これによって生成されたデータ構造を使用して  
シリアライズ・デシリアライズを行う。