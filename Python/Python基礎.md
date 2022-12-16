# Python基礎
## Pythonってなんだよ…
* Pythonはオブジェクト指向のスクリプト言語
* 動的型付け（変数を宣言したりするときには型を明示しない）
* AIとか情報処理とかの分野で活躍しているとされている
  - でも、もちろんwebをはじめとした他のところでも活躍！

* 文法が比較的シンプル
  - いわゆる「宗教戦争」が発生しにくい文法になっている
  - 学習コストも低め
* 標準ライブラリがとても充実している

### Pythonでできてるもの
* Django
  - Webアプリで使うフレームワーク

## Hello, World!
``` python
# coding: utf-8
print("Hello, World!")
```

とても簡単にできた。

## 基本的な文法
変数や関数の宣言・配列の作成などをまとめる。

### 変数の宣言・代入
``` python
# 数字とか文字列は普通に入る
a = 1
b = "test"
print(a) # -> 1
print(b) # -> test

# 再代入
a = 100
b = 200
print(a) # -> 100
print(b) # -> 200

# 配列は「[]」
c = [1, 3, 5, 7, 9]
print(c[1]) # -> 3
print(c[4]) # -> 9
```

* 型は明示しない
* 数値が入ってる変数に文字列を入れるとかも普通にできる（逆も然り）

### 条件分岐
``` python
a = 1
if a == 1:
	print("a = 1")
elif a == 2:
	print("a = 2")
else:
	print("a = ???")

b = "hoge"
if not b == "huga":
	print("b != huga")

c = 2
if a == 1 or c == 2:
	print("a == 1 || c == 2")
elif a == 1 and c == 2:
	print("a == 1 && c == 2")
```

* **「{}」は使わず**、**インデントでif文の中身を表現する**
  - 「宗教戦争」が起こらない理由のひとつ
  - 「{}」の代わりに`:`で区切る
* Pythonには **`switch`は存在しない**
  - 「辞書」を使うことである程度カバーはできる
* 否定を表す場合は「**not**」で表現する
* 「||」は「**or**」、「&&」は「**and**」で表現する

### ループ
``` python
# range関数を使うと連番になった数字の配列を取得できる
# この例では[1, 2, 3, 4, 5]が取得される
for i in range(0, 5):
	print(i) # -> 1から5が順番に出力される
	
array = ["hoge", "huga", "piyo"]
for content in array:
	print(content) # -> 「hoge」「huga」「piyo」が順番に出力される
```

### 関数の宣言
「def」で関数を宣言できる。  

``` python
def sum(a, b)
	result = a + b
	return result

# 関数名(引数)の形で呼び出し
c = sum(3, 5)
print(c) # -> 8
```

* Python全般に言えることだが、**「{}」は使わず**、**インデントで関数やif文の中身を表現する**。
  - 「宗教戦争」が起こらない理由のひとつ


## 参考資料
【Python入門】いまさらだけどパイソニスタとして必要な文法を網羅してみた  
<https://qiita.com/gold-kou/items/9713f6fd82baf1eccd6a>