## 参考資料
[Android App Bundle について](https://developer.android.com/guide/app-bundle)

## Android App Bundle(AAB)とは
アプリのコード(コンパイル済み)と各種リソースが含まれたファイル。
`apk`と似ているが少し違う。

これを`GooglePlay`に提出すると、それをもとに`GooglePlay`が`apk`を生成する。  
簡単に言うと「`apk`の素」だろうか。

## AABの特徴
* `GooglePlay`が各デバイス設定に合わせた`apk`を生成・配信してくれる
  - 開発者側でたくさん`apk`をビルドする必要がない
* ユーザーも必要なコードとリソースだけが入った`apk`をダウンロードすることになるため、
  容量が比較的軽くなる
* アプリ容量の限界が少し増える
  - 通常の`apk`は限界100MBに対して、`AAB`なら150MBまでOK
* 端末に直接入れることはできない
  - `apk`を生成して、初めて端末にインストールできる
  - `Android Studio`や`CLI`により、ローカルで`apk`を生成可能

## AABを始める
1. `Android Studio`(3.2以上)をインストール
2. アプリを`Play Feature Delivery`に対応させる
3. `Android Studio`または`CLI`で`AAB`を生成
4. 生成した`AAB`をテスト
5. `AAB`をGooglePlayに提出・公開