## rmコマンド
ファイルの削除を行う。  
オプション指定によりディレクトリの削除も可能。

rmで削除したファイルやディレクトリは復活できないため、  
コマンドの扱いには注意が必要。

## 基本の使い方
```bash
rm [オプション] [削除するファイル]
```

## ディレクトリの削除
```bash
$ tree 
.
|-- hoge.txt
`-- testdir
    `-- test.txt


$ rm -r testdir
rm: descend into directory 'testdir'? y
rm: remove regular empty file 'testdir/test.txt'? y
rm: remove directory 'testdir'? y

$ ls
hoge.txt
```

`-r`を指定することで、ディレクトリ以下のファイルを再帰的に削除する。  
（ディレクトリ内にさらにディレクトリがあった場合はその中のファイルも対象）

最後にディレクトリ自体の削除も確認され、`y`で削除可能。

## 強制削除
```bash
rm -f test.txt
```

`-f`を指定すると、確認なしで削除を行える。  
シェルスクリプト等でいちいち確認を踏みたくない場合に有効だが、  
通常の操作で使うのは危険なのであまり推奨されない。