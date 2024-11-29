<https://gihyo.jp/article/2022/08/ganshiki-soushi2-0042>

bashでは`{}`内に固有の記述をすることで、  
中に含まれる要素を反復展開できる。

* `{,}`: 個別に展開
	- `,`の手前に何も書かないパターンも可能（空文字で展開される）
```bash
echo 2024-09-01.{txt,tsv}
# 2024-09-01.txt 2024-09-01.tsv

echo {,bk_}hogehoge.txt
# hogehoge.txt bk_hogehoge.txt
```

* `{..}`: 1ずつ増やして展開
```bash
echo 2024-09-{01..03}
# 2024-09-01 2024-09-02 2024-09-03
```