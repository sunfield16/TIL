SearchBuilderはDataTablesの拡張機能の1つ。  
少しのコードの追加で以下のような一般的なテーブル内検索機能が設置できる。

* カラムごとの検索機能
  - 一致・不一致
  - 以上・以下
  - 数値などの範囲指定
  - 文字列のプリフィックス・サフィックス検索
  - ある文字列を含む・含まない
  - 空白・空白ではない
* ↑を組み合わせた複数条件の検索（and, or）

また、コード上での各種パラメータ設定により検索フォームの調整や  
さらに複雑な検索も可能。

[公式サイト](https://datatables.net/extensions/searchbuilder/examples/)に、条件指定方法や  
カスタマイズした例も用意されている。

## 導入
[公式サイト](https://datatables.net/download/)からダウンロードする時に、  
Extensionで指定しておくと追加でダウンロードできる。  

### 日付を扱う場合の注意
テーブルで日付を扱う場合、別のExtensionである`DateTime`も  
一緒にダウンロードする必要がある模様。

https://datatables.net/forums/discussion/76107/searchbuilder-requires-datetime-when-used-with-dates

## 基本の使い方
一般的なテーブル内検索機能を追加するだけであれば、初期化時に以下を指定するだけでOK。
```javascript
// DataTable の初期化時に dom で指定する
$('#test-table').DataTable( {
    dom:'Qfrtip'
} );
```