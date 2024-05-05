## fieldset
https://developer.mozilla.org/ja/docs/Web/HTML/Element/fieldset

`form`内の要素をまとめてグループ化するのに使われる。  
`label`などに似てるが、こっちはブロック要素。

* `form`属性に対象のフォームのIDを入れることで、`form`タグの外にあるinputなどを送信内容に紐づけられる
* `disable`属性により、そのfieldsetの中にある全てのinputなどを一括で無効化できる

## legend
`fieldset`の中に含めることで、その`fieldset`の見出しとして扱う。


```html
<form action="#">
  <fieldset>
    <legend>猫は好き？</legend>
    <input type="radio" id="like" name="likecats" value="like" /> <label for="like">Yes</label>
    <input type="radio" id="dislike" name="likecats" value="dislike" /> <label for="dislike">No</label>
  </fieldset>
</form>
```