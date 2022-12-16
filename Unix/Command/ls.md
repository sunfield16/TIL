## lsコマンド
指定のディレクトリの中身やファイルを一覧で表示する。

ファイルの名前だけでなく、サイズやパーミッションなどの各種詳細も表示可能。  
ワイルドカードによる絞り込みもできる。

## 基本の使い方
```bash
ls [オプション] [ディレクトリ・ファイル名]
```

ディレクトリの指定がない場合は現在のディレクトリの内容が表示される。

## ディレクトリの中身を表示する
```bash
# 「/hogehoge/data」に入っているファイルを表示
ls /hogehoge/data
```

## 絞り込み
```bash
# 「/hogehoge/data/」の中で「test〇.txt」のような名前のファイルを表示
ls /hogehoge/data/test?.txt

# 「/hogehoge/data/」の中で、拡張子が`.txt`のファイルを表示
ls /hogehoge/data/*.txt
```

ワイルドカードは「?」で1文字、「*」で任意の文字列（0文字でもOK）を表す。  
ディレクトリの中身がいっぱいあったりして探すのが面倒な場合等に有効。

## 詳細情報の表示
```bash
ls -l
```

`-l`でファイルの詳細情報を表示できる。

```bash
# 出力例
-rw-r--r-- 1 root root 120 May  4 08:33 temp.txt
```

## 隠しファイル(dotfile)の表示
```bash
ls -a /home/hoge
```

`-a`を指定すると隠しファイルを含めて表示できる。

```bash
# 出力例
.bash_profile  .bashrc  temp.txt  temp2.txt
```

## ソートして表示
```bash
# 更新時間の新しい順にソート
ls -t

# ソートの結果を逆順にする
ls -r
```

それぞれ指定することで、ファイルの表示順をソートできる。

## ディレクトリの情報を表示
ディレクトリが指定されている場合、  
その中にあるディレクトリの中身も表示するようになっている。
```bash
ls -l *

# 出力例
# ディレクトリ(hoge)は中身が表示されている
-rw-r--r--   1 fuga  staff    29  6 22 11:57 foo.txt
-rw-r--r--   1 fuga  staff    32  6 22 11:57 bar.txt

hoge:
-rw-r--r--  1 fuga  staff   29  6 22 11:57 temp.txt
-rw-r--r--  1 fuga  staff   32  6 22 11:57 temp2.txt
-rw-r--r--  1 fuga  staff   28  6 22 11:57 temp3.txt
```

この場合は `-d`でディレクトリ自体の情報を表示できる。
```bash
ls -l -d *

# 出力例
-rw-r--r--   1 fuga  staff    29  6 22 11:57 foo.txt
-rw-r--r--   1 fuga  staff    32  6 22 11:57 bar.txt
drwxr-xr-x   7 fuga  staff   224  6 21 18:36 hoge
```

## ディレクトリのみを表示
`-d`を利用して、ディレクトリのみを表示させることも可能。  
`/`をディレクトリ指定の最後につける。

```bash
ls -l -d */

# 出力例
# 普通のテキスト等は表示されない
drwxr-xr-x   7 fuga  staff   224  6 21 18:36 hoge/
```
`-d`だけ付ければ、ディレクトリ名だけを取得できる。  
シェルスクリプト等で有用。
```bash
ls -d */

# 出力例
hoge/
```
