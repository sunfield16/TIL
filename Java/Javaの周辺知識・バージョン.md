## 参考
https://www.sejuku.net/blog/12902

https://www.fenet.jp/java/column/java_beginner/6180/

https://qiita.com/nowokay/items/c1de127354cd1b0ddc5e

## Java SE
`Java Platform, Standard Edition`の略で、多くのJavaプラットフォームで使われる  
基本的なAPIの仕様をまとめたもの。

仕様書のようなイメージ。

## EE
`Jakarta Enterprise Edition`の略で、`Java SE`に加えて  
アプリケーションサーバーで使用される各種機能の規格を定めたもの。

`Java SE`の拡張仕様のようなイメージ。

## JRE
`Java Runtime Environment`の略で、Javaの実行環境。  
`JRE`がなければJavaを実行することはできない。

逆に、Java製のアプリケーションを実行するだけであればJREだけでも十分と言える。

## JDK
`Java Development Kit`の略で、Java製のアプリケーションを開発する際に  
必要な開発環境。`JRE`が内包されている。

JDKには公式のものとオープンソースのものがある。

### OracleJDK
Javaの商標登録元であるOracle公式のJava開発環境。  
商用利用の場合には有償になる。

### OpenJDK
JavaSEに基づいた実装のオープンソースプロジェクトによって作成されたJDK。  
色々な企業が開発・ビルドを行なっており、その分種類がある。

こちらはオープンソースであるため、無償で利用可能。  
Oracleがビルドを行なったOpenJDKもある。（`Oracle Open JDK`）

## バージョン番号
`java`コマンドで確認可能。
```bash
java -version
```

```
# 出力例
java version "1.8.0_131"
Java(TM) SE Runtime Environment (build 1.8.0_131-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)
```

バージョンに表示される番号は`JDK 8`とそれ以降で大きく変わっているため、  
注意が必要。

`JDK 8`以前
```
1.[メジャーバージョン].0_[マイナーバージョン]

例: JDK 8、マイナーバージョン1の場合
1.8.1
```

`JDK 8`以降
```
[メジャーバージョン].0.[マイナーバージョン]

例: JDK 11、マイナーバージョン2の場合
11.0.2
```