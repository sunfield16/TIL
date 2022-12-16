## mkdirコマンド
ディレクトリを作成する。  
基本的には1階層ずつしか作れないが、オプションにより  
深い階層までまとめて作成することも可能。  

## 基本の使い方
```bash
mkdir [オプション] [ディレクトリ名]
```

存在しないディレクトリに作成しようとするとエラーになる。

## 複数階層を一気に作成
```bash
$ tree
.
`-- testdir
    `-- test.txt

$ mkdir -p testdir/hoge/huga

$ tree
.
`-- testdir
    |-- hoge
    |   `-- huga
    `-- test.txt
```

`-p`を指定することで、上位のディレクトリも一気に作成できる。

---

## rmdirディレクトリ
ディレクトリを削除する。  
このコマンドでは空のディレクトリしか削除できない。  
（中身のあるディレクトリを削除する場合は`rm -r`で行う）

`mkdir`と同様に、オプションによって深い階層のディレクトリを  
一気に削除できる。

## 基本の使い方
```bash
rmdir [オプション] [ディレクトリ名]
```

## 複数階層を一気に削除
```bash
$ tree
.
`-- testdir
    |-- hoge
    |   `-- huga
    `-- test.txt

$ rmdir -p testdir/hoge/huga
rmdir: failed to remove directory 'testdir': Directory not empty

# testdirは空ではないので削除されなかった
$ tree
.
`-- testdir
    `-- test.txt
```

`-p`を指定することで、上位のディレクトリも一気に削除できる。  
ただし空のディレクトリでないと削除できないため、  
どこかの階層にファイルがある場合はそのディレクトリまで削除される。