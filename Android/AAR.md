https://developer.android.com/studio/projects/android-library?hl=ja

`Android ARchive`の略で、Androidのリソースや  
Manifestファイルを含めることができるパッケージファイル。

## ネイティブのコードを含める
内容物としてC/C++のコードも含められる。  
含める場合には共有ライブラリ（`.so`）を入れるのが基本。

AARはリソースやライブラリをパッケージとして扱うものであり、  
ビルドプロセスの中でリンクする必要がある静的ライブラリ（`.a`）を  
扱うのには向いていない。