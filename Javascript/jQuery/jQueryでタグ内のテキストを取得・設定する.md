jQueryでタグ内のテキストを取得・設定する場合にはいくつかメソッドがある。  
```html
<!-- この「hogehoge」を取得したり設定したい -->
<div>hogehoge</div>
```

## `html()`
内容をhtmlとして取得・設定する。  
htmlタグが含まれていれば、それはタグとして解釈される。  
（例えば`b`タグが入っていたらそこは太字になる）

## `text()`
内容を単純なテキストとして取得・設定する。  
htmlタグもただの文字列になる。

## `val()`
`value`属性の内容を取得・設定する。  
主に`input`タグの内容物に有効？

## 例
```html
<div id="id-html"><b>html()で取得・設定</b></div>
<div id="id-text"><b>text()で取得・設定</b></div>
<div id="id-val"><b>val()で取得・設定</b></div>
```

```javascript
console.log("html()で取得: " + $("#id-html").html());
console.log("text()で取得: " + $("#id-text").text());
console.log("val()で取得: " + $("#id-val").val());

// ボタンを押した時に以下を実行するように調整
$("#id-html").html("<u>html()で設定</u>");
$("#id-text").text("<u>text()で設定</u>");
$("#id-val").val("<u>val()で設定</u>");
```

```
html()で取得: <b>html()で取得・設定</b>
text()で取得: text()で取得・設定
val()で取得: 

ボタンを押したら以下のような表示になる
html()で設定 <- 下線
<u>text()で設定</u>
val()で取得・設定 <- 太文字
```


## 参考
<https://api.jquery.com/html/#html>  
<https://api.jquery.com/text/#text>  
<https://api.jquery.com/val/#val>  
<https://narunaru7638.hatenablog.com/entry/2019/04/13/002524>