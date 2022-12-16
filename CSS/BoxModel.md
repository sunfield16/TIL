## ボックスモデル
ボックスモデルはHTMLにおいてブロックボックスの要素が  
どのように表示されるかを決定するもの。

* ContentBox
* PaddingBox
* BorderBox
* MarginBox

の4つから構成される。

## ContentBox
そのコンテンツの表示領域を表す。  
`width`や`height`などのプロパティで調整できる。

## PaddingBox
コンテンツの外側にパディングとして用意された領域。  
（ここには何も表示されない）

`padding`関連のプロパティで調整できる。

## BorderBox
ContentBoxとPaddingBoxをラップする領域。  
境界線の表示はこのボックスの周囲になる。  

`border`関連のプロパティで調整できる。

## MarginBox
最も外側の領域で、コンテンツと他の要素の間隔を  
調整する役割を持つ。  
（ここには何も表示されない）

`margin`関連のプロパティで調整できる。