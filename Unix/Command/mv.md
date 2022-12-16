## mvコマンド
ファイルやディレクトリを他の場所へ移動する。  
名前の変更を行うことも可能。

## 基本の使い方
```bash
mv [オプション] [移動元のファイル・ディレクトリ] [移動先のファイル・ディレクトリ]
```

## 名前の変更
```bash
$ ls
test.txt

$ mv test.txt test2.txt

$ ls
test2.txt
```

移動先のファイルやディレクトリが存在しない場合、  
移動元のファイルやディレクトリがその名前に変更される。

## ディレクトリに移動
```bash
$ ls
test.txt testdir

$ mv test.txt testdir

$ ls testdir
test.txt
```

移動先にディレクトリを指定すると、そのディレクトリの中に移動する。  
移動元がディレクトリの場合も問題なく移動可能。

### 移動できない例
```bash
$ tree 
.
|-- test.txt
`-- testdir

# これはできない
$ mv test.txt testdir/testdir2/test.txt
mv: cannot move 'test.txt' to 'testdir/testdir2/test.txt': No such file or directory

# これはできる（移動後は名前が「testdir2」のファイルになる）
$ mv test.txt testdir/testdir2
```

## 上書き確認
```bash
$ ls
test.txt test2.txt

# yで続行、nでキャンセル
$ mv -i test.txt test2.txt
mv: overwrite 'test2.txt'? y

$ ls
test2.txt
```

移動先のファイルやディレクトリが既にある場合は上書きするが、  
`-i`を指定しておくと上書き時に確認してくれる。