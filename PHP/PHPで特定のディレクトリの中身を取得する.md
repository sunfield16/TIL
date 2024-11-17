## `glob`
手っ取り早いしコード量も少なく済む。  
重いのが欠点。

## `scandir`
ソート機能を持つ。  
globよりも高速化が期待できる。

##  `opendir, readdir`
globより高速だが、`closedir`忘れに注意が必要

## `RecursiveDirectoryIterator` 
Iteratorクラスとforeachを利用する形。  
`RecursiveIteratorIterator`も組み合わせることで、  
ディレクトリの中身を再帰的に走査できる。

また、ファイルパス以外の情報も取得可能、ただし記述量は多くなりがちかも

##  `exec + find`
`find`コマンドによる検索・絞り込みを行う。  
非常に高速とされている。

シェルを使う都合でlinux限定。また、インジェクションに注意が必要

## 参考
<https://blog.ver001.com/php-glob-opendir-comparison/>  
<https://qiita.com/fallout/items/1f8a9bd044b09b1b3d66>  
<https://www.php.net/manual/ja/class.recursivedirectoryiterator.php>