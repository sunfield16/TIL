## figure
https://developer.mozilla.org/ja/docs/Web/HTML/Element/figure

画像や図表など1つで自己完結する要素を表す。  
本文の流れから参照されるが、付録などに移動されても問題ないものに使うイメージ。

## figcaption
`figure`の中に`figcaption`を含めることで、  
`figure`に含まれるコンテンツを説明する文書を表す。

```html
<figure>
	<img src="hogehoge.jpg">
	<figcaption>これはなにかしらの画像の説明です</figcaption>
<figure>
```