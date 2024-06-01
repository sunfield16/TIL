https://redis.io/  
https://github.com/redis/redis

インメモリで動作するNoSQLデータベースの1つ。
インメモリのため高速な読み書きが可能で、キャッシュ機構や  
データベースとしての利用など幅広い用途に使われている。

また、以下のような幅広いデータ構造をサポートしている。

* 単純な文字列（String）
* 連想配列（Key/Value）
* リスト
* セット（集合）
* 地理空間
* ビットマップ・ビットフィールド

## 特徴
* 不揮発性のため、永続性を確保するには他の場所にデータを移す必要あり
	- その点もスナップショット機能などが入っているのでやりやすい
* レプリケーション機能により可用性が高い
	- マスター/スレーブ機構
* ベクターデータベースなどもサポートしていて、ドキュメントやWikiなどの検索にも強い

## vs Memcached
https://zenn.dev/marshmallon/articles/27e279e41a98d6  
https://yakst.com/ja/posts/3243

似たような機能を持つデータベースに`Memcached`があるが、  
比較するとRedisは以下の点で異なる。

### 強み
* データ構造のサポートがある（Memcachedは文字列のみ）
* 永続性の確保がしやすい

### 弱み
* Memcachedに比べるとメモリのオーバーヘッドが大きい
* シングルスレッドで動作（Memcachedはマルチスレッド）
	- どちらかといえばMemcachedのほうがスケーリングが簡単
* いろいろある分、Memcachedよりも覚えることが多くて複雑



## 記法
特にRedisをCLIから触る場合は以下のような書き方をする。

### 単純な文字列
```redis
SET [キー] [値]
SET hoge fuga

GET hoge
# 出力: fuga
```

### 連想配列
```redis
HSET [キー] [配列のキー] [値] [配列のキー] [値] ...
HGET [キー] [配列のキー]
HGETALL [キー]

HSET user name hoge age 23
HGET user name
# 出力: hoge

HGETALL user
# 出力: ↓のようになる
1) "name"
2) "hoge"
3) "age"
4) "23"
```