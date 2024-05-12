## コンテナが特殊プロセス扱いのケース
https://qiita.com/sun33/items/d62744f5746f6815f3c8  
https://text.superbrothers.dev/200328-how-to-avoid-pid-1-problem-in-kubernetes/

コンテナが特殊なプロセス扱いになっていて終了できない模様。  
`compose.yaml`にinitを追加することで対策できる。
```yaml
services:
  app:
	~~省略~~
	# ↓を追加する
    init: true
```