[[Telnet]]で接続して諸々確認したい時に使う。  
以下のようにechoから繋げることでワンライナーにすることが可能。
```bash
(echo "stats"; sleep 0.5s;) | telnet localhost 11211
```

## キーの内容取得
```telnet
get [キー名]

# 例
get hogehoge_key          
VALUE hogehoge_key 0 6
184258
END
```

## 統計の取得
キャッシュのヒット率やセットされた数など、現在の各種統計情報が確認できる。
```telnet
stats
STAT pid 3641
STAT uptime 334765
STAT time 1693194615
STAT version 1.4.22
STAT libevent 1.4.14b-stable
STAT pointer_size 64
STAT rusage_user 3.000388
STAT rusage_system 5.601408
STAT curr_connections 33
STAT total_connections 157
STAT connection_structures 35
STAT reserved_fds 160
STAT cmd_get 9442
STAT cmd_set 4482
STAT cmd_flush 0
STAT cmd_touch 0
STAT get_hits 4919
STAT get_misses 4523
STAT delete_misses 0
STAT delete_hits 0
...
```

## 全キャッシュの削除
メモリが解放されるわけではなく「全キャッシュを期限切れにする」という挙動。
```telnet
flush_all
```

## 参考
<https://github.com/memcached/memcached/wiki/Commands>  
<https://changineer.info/server/nosql/nosql_memchached_commands01.html>  
<https://qiita.com/TatsuNet/items/5c89a2dbce57be28aef7>