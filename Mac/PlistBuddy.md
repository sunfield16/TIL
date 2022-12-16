## PlistBuddy
`plist`を編集できるコマンド。Macに標準搭載されている。

シェルスクリプト等で`plist`を触りたい場合に、  
簡単な構文で`plist`を編集できるので便利。

## 使い方
```bash
$ /usr/libexec/PlistBuddy -c [編集構文] [編集するplist]
```

## 編集構文
| コマンド | 内容 |
| ---------|---------- |
| add [要素名] [型] [設定値] | 要素を追加する |
| set [要素名] [設定値] | 要素に値を設定する |
| print [要素名] | 要素の内容を表示する |

## 型
`plist`の型に準ずる。

| 型名 | 内容 |
| ---------|---------- |
| string | 文字列 |
| integer | 数値 |
| bool | true/false |

## 使用例
* string型の要素「foo」（内容: bar）を追加する
```bash
$ /usr/libexec/PlistBuddy -c "add foo string bar" ./hoge.plist
```

* integer型の要素「piyo」に「3」を設定する
```bash
$ /usr/libexec/PlistBuddy -c "set piyo 3" ./hoge.plist
```