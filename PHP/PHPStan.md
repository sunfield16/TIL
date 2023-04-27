## 参考
https://zenn.dev/tadsan/articles/00bf49f8ec2f16  
https://qiita.com/rowpure/items/e1aa3384c903e7a335ec

## PHPStan
PHPStanはPHPの静的解析ツールの1つ。  

* シンタックスエラー
* 変数や関数の未定義
* 引数の数をチェック
* PHPDocs記法の確認
  - 記述と実際の関数定義とかに差異があると指摘される

など、ソースコード上でよろしくない記述がないか  
チェックを行ってくれる。

## 解析レベル
PHPStanでは指摘する項目をレベルで指定できる。  
数値が高くなるほど項目が増えて厳密なチェックが可能。  
（上のレベルは下位のレベルの項目も含まれる）

# 使用方法
## インストール・実行
`composer`を使用しているプロジェクトであればインストールは簡単。
```bash
composer require --dev -W phpstan/phpstan phpstan/extension-installer
```
解析する場合はインストールされたバイナリを実行する。
```bash
# composerのディレクトリにいる状態から実行
./vendor/bin/phpstan analyze [各種オプション]
```

## オプション指定
各種オプションによって解析レベルの調整やディレクトリ指定を行える。  
これらは設定ファイルでも指定できるので、  
CI等で使う場合は設定ファイルを用意するのが良い。

解析時に使う設定ファイルは`-c`で指定する。
```bash
./vendor/bin/phpstan analyse -c phpstan.neon
```

## 設定ファイル
設定ファイルは`.neon`という拡張子のファイルで指定する。  
中身は[yaml](/Serialization/YAML.md)形式で記述可能。

また、ファイル内のパス指定は設定ファイルがあるディレクトリからの相対パスになる。

### 設定例
```yaml
parameters:
	level: 1
	paths:
		- src
		- hoge/fuga
	fileExtensions:
		- php
		- inc
	excludePaths:
		analyse:
			- src/thirdparty
		ignoreErrors:
			- '#Result of function [a-zA-Z0-9\\_]+ \([a-zA-Z0-9\\_]+\) is used\.#'
```

### level
解析レベルを指定する。（0〜9）

### paths
解析対象のパスを指定する。  
ディレクトリを指定すると、その中にあるパス以下のファイルは全て対象になる。

### fileExtensions
解析対象の拡張子を指定する。  
`.php`だけでなく`.inc`などで書かれたファイルも対象に含めることが可能。

### excludePaths
解析対象から外すパスを指定する。

### ignoreErrors
指摘項目から外す内容を指定する。  
「都合上どうしても出てしまうけど許容するもの」などを指定するのが良さそう。