## grepでor, and, not検索
### or検索
`-e`で複数ワード検索ができる。
```bash
grep -e "hoge" -e "fuga" ./test.txt
```

### and検索
andはgrep1回ではできないので、素直にパイプでつなげる。
```bash
grep "hoge" ./test.txt | grep "fuga"
```

### not検索
`-v`で除外の指定ができる。  
指定したワードがない行が出力される。
```bash
grep -v "hoge" ./test.txt
```