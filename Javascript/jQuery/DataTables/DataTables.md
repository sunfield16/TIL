DataTablesはjQueryのプラグインの1つ。

`<table>`を使う際に見た目を簡単にわかりやすくしたり  
汎用的な機能を提供してくれる。

* ソート
* ページング
  - 1ページあたりの表示数も操作できる
* 検索
  - テーブル全体
  - テーブルのカラム単位
* ソートや検索時のイベントハンドリング
  - コールバックを指定しておくと各タイミングで処理が呼ばれる

## 導入
* CDNでスクリプトを導入する
* 公式サイトからスクリプトをダウンロードして配置
* npm

などで導入可能。

## 基本の使い方
`<table>`にidを設定しておき、jQueryでそのセレクタを読み込んで初期化すれば  
DataTablesでの管理ができるようになる。
```html
<table id="test-table">
	<thead>
		<tr>
			<th>ID</th>
			<th>name</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>1</td>
			<td>hoge</td>
		</tr>
		<tr>
			<td>2</td>
			<td>huga</td>
		</tr>
		<tr>
			<td>3</td>
			<td>piyo</td>
		</tr>
		<tr>
			<td>4</td>
			<td>foo</td>
		</tr>
		<tr>
			<td>5</td>
			<td>bar</td>
		</tr>
	</tbody>
</table>
```
```javascript
$(document).ready(function () {
	// DataTable()で初期化する
    const test_table = $('#test-table').DataTable();
});
```

## 翻訳
DataTablesで生成されるUIは基本的に英語になっているが、翻訳用のjsonを読み込ませることで  
ローカライズが可能。（もちろん日本語化も）

```javascript
const test_table = $('#test_table').DataTable({
    language:{
        url: "[jsonを配置したパス、もしくはURL]"
    }
});
```

有志によって各言語で翻訳が進められており、  
[公式サイト](https://datatables.net/plug-ins/i18n/)には各言語で使えるjsonが用意されている。