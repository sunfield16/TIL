<https://www.php.net/manual/ja/language.operators.logical.php>
<https://www.php.net/manual/ja/language.operators.precedence.php>

`or`演算子を使うとこういう書き方ができる。
```php
$file = fopen("./hoge.txt", "r") or exit("ファイルが開けませんでした");

// 実質これと同じ
if(!($file = fopen("./hoge.txt", "r")))
{
	exit("ファイルが開けませんでした");
}
```

なお、`||`も使えるが、こっちでは機能しない。  
`||`は`=`（代入）よりも先に処理されてしまう。

```php
// false || true を先に処理してから、
// その結果を $a に代入する
// （$a は true になる）
$a = false || true

// $a = false の代入を先に処理してから、
// $a or true を処理する
// （$a は false のまま）
$a = false or true;
```

ただし、処理順を考慮する必要があるため、基本的には  
使わない方が良いのではないかとは思う。  
（見かけた場合に理解できるようにはしたい）