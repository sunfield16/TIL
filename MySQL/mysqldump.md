MySQL公式のユーティリティコマンド。  
データベースやテーブルの内容をSQLやCSVとして書き出すことができる。  

主に、特定のMySQLデータベースから他のサーバーにあるMySQLに  
データをそっくりコピーするような場合に使われる。

## 基本の使い方
```bash
# 特定のdatabaseの中身を出力
mysqldump -u [MySQLユーザー名] -p -h [ホスト] [database名] > [出力先ファイル]

# 特定のdatabaseの、特定のtableの中身を出力
mysqldump -u [MySQLユーザー名] -p -h [ホスト] [database名] [table名] > [出力先ファイル]
```

## 複数のテーブルのdump取得
データベース名の後にテーブル名を複数並べられる。
```bash
mysqldump -u hoge -p -h 000.000.000.000 database_hogehoge table_aaa table_bbb
```

どれがデータベースでどれがテーブルかを明示的に書きたい場合は、  
`--databases`と`--tables`を使う。  
```bash
mysqldump -u hoge -p -h 000.000.000.000 --databases database_hogehoge --tables table_aaa table_bbb
```
※正確にはこれらのオプションは、「ここから先の名前引数を全部データベース/テーブル名として扱う」というもの。

## 特定のテーブルだけを無視する
`--ignore-table`で「このテーブルだけdumpいらない」を指定できる。  
データベース名とテーブル名の両方を指定する必要あり。

もし複数テーブルを無視したい場合はその分だけオプション指定が必要。
```bash
mysqldump -u hoge -p -h 000.000.000.000 --ignore-table=database_hogehoge.table_aaa --ignore-table=database_hogehoge.table_bbb database_hogehoge
```

## テーブルの設計だけ取得
`--no-data`を指定すると、中身は取得せず設計だけを取得できる。  
ユーザーデータ関連のテーブル設計を他のサーバーに持っていきたいような場合に有効？

## テーブルの中身だけ取得
`--no-create-info`を指定すると、設計を取得せず中身だけを取得できる。  
`DROP TABLE`と`CREATE TABLE`は出力されない。


## エスケープ処理を行う
`--quote-names`を指定することでカラム名などをエスケープすることができる。  
カラムやテーブル名でエスケープしなければならないものがある場合に有効。  

MySQL5.7 -> 8.0 への移行では`rank`が予約語になった関係で、  
`rank`という名前のカラムを含むテーブルがあると  
エスケープする必要が出たりした。


## 参考
https://dev.mysql.com/doc/refman/8.0/ja/mysqldump.html  
https://qiita.com/PlanetMeron/items/3a41e14607a65bc9b60c