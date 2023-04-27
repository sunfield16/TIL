PHPで`mkdir`関数を使う時、パーミッションを指定できる。  
ただし、指定によっては想定したパーミッションにならない場合がある。
```php
<?
# パーミッション 0777 でディレクトリを作成する
mkdir(__DIR__."/hoge", 0777);

# パーミッションを確認
$perm = decoct(fileperms(__DIR__."/hoge") & 0777);
echo($perm.PHP_EOL);

# 出力（777が出るはずだが異なっている）
# 755
```

## 原因
この`mkdir`関数は、設定している[umask](/Unix/Command/umask.md)の影響を受ける。

umaskには多くの場合デフォルトで`022`が指定されているため、  
パーミッションにマスクがかかり想定したものと異なるパーミッションになる。

## 対策
### chmod
ファイル作成時、同時にchmodする。
```php
$dir = __DIR__."/hoge";
mkdir($dir, 0777);
chmod($dir, 0777);
```

ただし、再帰的にディレクトリを作成するときは  
作成した全ディレクトリに対して変更を行う必要がある。
```php
# この場合は hoge/fuga/piyo だけが 0777 になってしまう
$dir = __DIR__."/hoge/fuga/piyo";
mkdir($dir, 0777, true);
chmod($dir, 0777);
```

### umaskを変更する
1つの方法だが、これは他にPHPを実行しているとそちらにも影響するため  
推奨されない。
```php
# いったん umask を 0 にする
umask(0);
mkdir(__DIR__."/hoge", 0777);
```

## 参考
https://www.php.net/manual/ja/function.mkdir.php  
https://nodoame.net/archives/5400