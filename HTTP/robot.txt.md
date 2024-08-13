https://developers.google.com/search/docs/crawling-indexing/robots/intro?hl=ja  
https://developers.google.com/search/docs/crawling-indexing/block-indexing?hl=ja  
https://gmotech.jp/semlabo/seo/blog/robotstxt_method/

特定のWebページなどに対する検索エンジンのクローラー巡回を  
制御するための設定ファイル。  
これを配置することで、以下のような制御ができる。

* このディレクトリ以下はクローラー巡回を禁止
* 特定のクローラーだけ巡回を禁止

クローラーを制御しても検索エンジン上に表示されないわけではなく  
他のページからリンクされていると表示される場合もある。  
そのためWebページを検索で引っかからないようにする目的で使用するのは良くないとされている。  

## noindexとの使い分け
似たような操作として、htmlにはmetaタグの`noindex`が存在する。  
それぞれやっていることが違うので、使い分けが必要。

* `robots.txt` ... クローラー巡回を禁止
	- ただし、検索結果に表示されないとは限らない
* `noindex` ... インデックスの禁止（検索結果に表示させない）
	- ただし、クローラー巡回はされる
		- 逆にクローラーが巡回しないと`noindex`が適用されない