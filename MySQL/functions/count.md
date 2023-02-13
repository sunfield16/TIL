SQL内で、主に集計で使われる関数。  
`SELECT`によって取得した行の中で、指定した文字列や式が  
**NULLではない**行の数を取得する。

基本はカラム名を指定するが、条件式なども指定可能。

## 基本の使い方
例では以下のテーブルを使う。
```sql
-- 以下のような生徒名簿テーブルがあるとする
CREATE TABLE students (
	student_id INT NOT NULL,    -- 生徒ID
	name VARCHAR(16) NOT NULL,  -- 名前 
	class VARCHAR(16) NOT NULL, -- クラス
	club VARCHAR(16)            -- 部活動（未所属の場合はNULLとする）
);
```

```sql
-- clubがNULLではない（＝部活動に所属している）生徒を数える
SELECT COUNT(club) FROM students;
```

`*`を指定すると、NULLかどうかに関わらず取得された行数を返す。
```sql
-- 全生徒の人数を取得
SELECT COUNT(*) FROM students;
```

## 重複を排除する
`DISTINCT`を使うことで、指定した文字列や式が重複しても1件として集計を行う。  

```sql
-- 名前ごとに1人としてカウント（＝名前の数を集計する）
SELECT COUNT(DISTINCT name) FROM students;
```

## 条件を指定する
条件を`COUNT`内で指定すれば、条件に当てはまるものだけを
ただし、想定した結果を取得するために`OR NULL`を条件に追加するのが無難。（後述）
```sql
-- 田中さんの人数を数える
SELECT COUNT(name = "田中" OR NULL) FROM students;
```

### `OR NULL`をつける 
MySQLでは、条件式の結果は基本的に **0 か 1** になる。  
ただし`COUNT`が集計するのは**NULLではない**行の数であるため、  
条件式をつけたとしても集計対象になってしまう。

そこで、`OR`の特性を利用して条件に当てはまらないものを  
NULLにする手法が取られる。

`OR`の仕様は以下のようになっている。

* 式の両方ともNULLではない ... どちらかの結果が 0 以外なら 1 を返す、それ以外の場合は 0
* 式のどちらかがNULL ... **どちらかの結果が 0 以外なら 1 を返す、それ以外の場合はNULL**
* 式の両方がNULL ... NULLを返す

これによって、条件に当てはまらない場合にNULLが返り  
`COUNT`の集計から除外することが可能になる。