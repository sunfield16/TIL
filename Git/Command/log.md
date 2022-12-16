## `git log`
そのリポジトリ内でのコミットログを確認できる。  
パラメータ指定により、様々な形でログを検索可能。

* 指定したファイルの変更履歴
* 指定した期間内に絞ったコミットログの確認
* 各コミットログを１行で出す

## 基本の使い方
```bash
# リポジトリ管理対象のディレクトリで実行する
git log [各種パラメータ]
```

## 表示方法の指定
### 1行で表示
各コミットを1行で表示する。
```bash
git log --one-line
```
```bash
# 出力
xxxxxxxxx (HEAD -> master, origin/master) コミット1
yyyyyyyyy コミット2
zzzzzzzzz コミット3
```

### ログと変更されたファイル（+変更の種類）を表示
ログに加えて、そのコミットで変更されたファイルの一覧を表示できる。  
変更の種類は追加(A)・修正(M)・削除(D)のどれか。
```bash
# ファイルのみ
git log --name-only

# ファイル+変更の種類
git log --name-status
```
```bash
# ファイルのみ出力
Path/To/File.txt
Path/To/File2.php
Path/To/File3.php

# ファイル+変更の種類出力
A       Path/To/File.txt
A       Path/To/File2.php
M       Path/To/File3.php
```

## 表示対象の指定
### 表示するコミットの数を指定
数字を指定するとその数までコミットが表示される。
```bash
# nは省略してもOK
git log -n3
git log -3
```