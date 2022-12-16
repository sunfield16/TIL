# gitをコマンドラインで使っていく
基本SourceTreeでしかgitを触ってないので決まったコマンド以外はあまり理解していない。  
これだとコマンドラインを使わざるを得ない状況のとき困るので、多少なりとも覚えていく。

## リポジトリを創造する
リポジトリを作らなければ何も始まらない。  
作るときは`cd`で移動してから行うこと。

``` bash
cd ~/Desktop/HogeHoge #作りたい場所に移動する。
git init
```

## 現状確認
`git init`することでリポジトリが作られた。  
githubとかだとだいたいREADME.mdがルートディレクトリに設置してあるので、適当に作成する。

作成が完了したところで、現在の状態を確認してみる。

``` bash
git status
```

これで下記のようにコミットされてないファイルや現在のブランチを雑に確認できる。

``` bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
```

## なんかコミットする
gitには「**ワークツリー（作業エリア）**」と「**ステージング**」の概念があり、  
コミットされるのは必ず「ステージング」のファイルのみになる。

変更がかかったファイルはまだ「ワークツリー」で管理されている状態なので  
これを「ステージング」で管理させる必要がある。  
そのためには`git add`を使う。

``` bash
git add README.md
```

これでさっき作った`README.md`がステージングに上がった。もう一度状態を確認すると、

``` bash
git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md

```
下の方がちょっと変わっている。これでファイルがステージングでの管理になった。

ワークツリーに戻したい場合は`git status`の説明にもあるように操作すれば戻せる。

``` bash
git rm --cached README.md
```

コミットするためには`git commit`を使う。

``` bash
# ファイルがステージングにある状態で
git commit -m "first commit"
```

**これで記念すべき初コミットの完成である。**  
`-m`を使うことで、コメントを設定できる。基本的にはこれを使うこと。

## ログを見る
初コミットができたところで、このリポジトリの歴史とも言えるログを確認してみる。  
`git log`で確認が可能。

``` bash
git log

commit 197831597025d07e8347b982d95ce06f63a40b43 (HEAD -> master)
Author: hogehoge
Date:   Fri Jul 5 11:20:43 2019 +0900

    first commit
```