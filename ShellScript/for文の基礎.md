## for文の基本構成
値リストは変数を指定してもいいし、直接文字列を羅列していってもいい。  
変数には値リストの中身が順番に入る。
```bash
for 変数 in 値リスト
do 
	処理
done
```

## 文字列を直接指定する場合
```bash
for each in "test1" "test2" "test3" "test4" "test5"
do 
	echo "in array: ${each}"
done
```
```bash
# 出力
in array: test1
in array: test2
in array: test3
in array: test4
in array: test5
```
## 変数を指定する場合
* スペース区切り
* tab区切り
* 改行

で区切られたものが入った変数であれば、for文でループ処理を行える。
```bash

# スペース区切り
readonly hoge="test1 test2 test3 test4 test5"

# tab区切り
readonly hoge="test1	test2	test3	test4	test5"

# 改行
readonly hoge=$(cat <<- EOC
	test1
	test2
	test3
	test4
	test5
	EOC
)

for each in ${hoge}
do
	echo "in array: ${each}"
done
```
```bash
# 出力
in array: test1
in array: test2
in array: test3
in array: test4
in array: test5
```


## コマンドを展開する場合
`seq`で1~10までの整数を順番に並べる。  
このコマンドを直接for文に渡しても問題なし。
```bash
for each in $(seq 1 10)
do
	echo "in array: ${each}"
done
```

```bash
# 出力
in array: 1
in array: 2
in array: 3
in array: 4
in array: 5
in array: 6
in array: 7
in array: 8
in array: 9
in array: 10
```