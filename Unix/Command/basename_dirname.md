## basename
`basename`は、指定のパスからファイル名だけを取得するコマンド。  
主にシェルスクリプトで使う機会があると思われる。

## dirname
`dirname`は、指定のパスからディレクトリ部分だけを取得するコマンド。  
`basename`と対照的な動きになる。

## 基本の使い方
```bash
basename [オプション] [ファイルパス]
dirname [オプション] [ファイルパス]
```

例としては以下のようになる。
```bash
basename "/path/to/file.txt"
dirname "/path/to/file.txt"
```
```
# 出力(basename)
file.txt

# 出力(dirname)
/path/to
```

## basenameで接尾辞を取り除く
`basename`は、`-s`で指定した接尾辞を削除して取得できる。  
主に拡張子がいらない場合に便利。

```bash
basename -s ".txt" "/path/to/file.txt"
```
```
# 出力
file
```

## 変数展開で同じ動きをする
変数展開には前方一致や後方一致で中身を除去して取得するものがあり、  
それを利用して`basename`や`dirname`と同じことができる。

ただし、可読性はあまり良くないので  
使い所は難しいかもしれない。

```bash
readonly DIR="/path/to/file.txt"

# 前方一致により、文字列の一番後ろの'/'から手前を全て除去して取得（basename）
echo "basename: ${DIR##*/}"

# 後方一致により、文字列の一番後ろの'/'から後ろを全て除去して取得（dirname）
echo "dirname:  ${DIR%/*}"
```

```
# 出力
basename: file.txt
dirname:  /path/to
```