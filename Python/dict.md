# dict
`dict`はいわゆる連想配列で、キーに対応する値を保存する。

## 生成・値の設定
```python
table = dict()

# [キー] = [値]でデータを登録
table["hoge"] = 1
table["fuga"] = 2
table["piyo"] = 3

# {}で生成と同時にデータ登録も可能
table2 = {"hoge":1, "fuga":2, "piyo":3}
```

## ループ
`items()`でキーと値の両方、`keys()`や`values()`で  
キーか値のみを取得できる。

```python
table = {"hoge":1, "fuga":2, "piyo":3}

for key, value in table.items():
    print("key:{0} value:{1}".format(key, value))

for key in table.keys():
    print(key)

for value in table.values():
    print(value)
```

## キーの存在確認
dictにキーが存在するかどうかを判定したい場合は
`[キー] in [dict名]`で行う。
```python
table = {"hoge":1, "fuga":2, "piyo":3}

if "hoge" in table:
    print("hoge is in table")

if not "foo" in table:
    print("foo is not in table")
```

## 複数のdictを合成する
`update()`を使うと、引数に指定したdictの内容を取り込むことができる。  
この時同じキーがあった場合は、引数に指定したdictの内容で上書きされる。

```python
table1 = {"hoge":1, "fuga":2, "piyo":3}
table2 = {"hoge":4, "foo":5, "bar":6}

table_updated = table1.update(table2)
# table_updatedの中身
# hoge: 4
# fuga: 2
# piyo: 3
# foo : 5
# bar : 6
```