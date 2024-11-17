<https://hub.docker.com/_/redis>

公式のDockerイメージがあるのでそれを活用できる。  
ページ内に導入や使い方の記載もあるので始めやすい。
```dockerfile
FROM redis:7.2.5-alpine
```

<https://kinsta.com/jp/blog/redis-docker/>  
この記事では、脆弱性の確認のしやすさやアプリとの切り離しの容易さから  
DockerとRedisの相性が良いことを伝えている。

## データの永続化
RDBの保存データはRedisコンテナ内の`/data`に保存されるため、  
↓のように`/data`をマウントしておくことで永続化できる。
```yaml
redis:
	volumes:
		- "./redis/dump:/data"
	ports:
		- 6379:81
	...
```
