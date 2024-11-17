## 関数の基本的な記述
```makefile
$([関数名] [引数1],[引数2],...)

# {}で囲む形でもOK
${[関数名] [引数1],[引数2],...}
```
関数は入れ子にすることも可能。
```makefile
# 今のディレクトリ内にあるcppを全部取得して、プリフィックスに`hoge/`を追加する
$(addprefix hoge/,$(wildcard *.cpp))
```

## `addprefix`, `addsuffix`
引数で指定した文字列を、第2引数で指定した文字列の先頭や最後につける。
```makefile
TEST_CPP = foo.cpp bar.cpp 
TEST_CPP_PRE = $(addprefix hoge/,$(TEST_CPP)) 
# hoge/foo.cpp hoge/bar.cpp
```

```makefile
TEST_DIR = foo/ bar/ 
TEST_DIR_SUF = $(addsuffix hoge.cpp,$(TEST_DIR)) 
# foo/hoge.cpp bar/hoge.cpp
```

## `wildcard`
ワイルドカードを使って指定のディレクトリにあるファイルを検索する。
```makefile
TEST_DIRS = $(wildcard ./*.cpp)
# foo.cpp bar.cpp
```


## 参考
<https://tex2e.github.io/blog/makefile/functions>