SQLにはデータを`insert`する方法が複数存在する。

## 通常のINSERT文
```sql
INSERT INTO user(name) values('test1');
INSERT INTO user(name) values('test2');
```

普通のINSERT文を並べる。  
しかし、これでは大量のINSERTが必要な場合にとても重い。

## BulkInsert（バルクインサート）
```sql
INSERT INTO user(name) values('test1'), ('test2'), ('test3');
```
1つのINSERT文に複数のデータを並べる。  
これなら同時に複数のデータを挿入できるため、高速化が期待できる。

## LOAD DATA INFILE文
```sql
LOAD DATA INFILE 'file_name' INTO TABLE db2.my_table;

-- MySQLのサーバーとファイルのあるサーバーが異なる場合はこうする
LOAD DATA LOCAL INFILE 'file_name' INTO TABLE db2.my_table;
```
`csv`からデータを取得し、テーブルに入れていく。

全てのフィールドに同じ文字セットが使われていないといけないが、  
INSERT文よりも高速でデータを挿入することが可能。
