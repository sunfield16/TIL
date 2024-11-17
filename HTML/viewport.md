<https://developer.mozilla.org/ja/docs/Web/HTML/Viewport_meta_tag>  
<https://gmotech.jp/semlabo/seo/blog/howto-viewport/>

metaタグで指定できる要素の一つで、Webページを見られる表示領域を表す。  
ブラウザでWebページを開いたとき表示されている範囲がviewport。

以下のように設定する。
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## 設定できる項目
* width ... 横のサイズを指定する
	- ピクセル数か`device-width`を指定
	- `device-width`を指定すると100vwと同じになる
* height ... 縦のサイズを指定する
	- ピクセル数か`device-height`を指定
	- `device-height`を指定すると100vhと同じになる
* initial-scale ... ページを最初に読み込んだ時の表示倍率を指定する
	- 0.1 ~ 10の範囲。デフォルトは1