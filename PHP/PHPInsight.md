## 参考
<https://qiita.com/yasuaki640/items/9684d450613a1c6d0234>  
<https://phpinsights.com/get-started.html>

## PHPInsight
`PHPInsight`はPHPの静的解析ツールの1つ。  
ソースコードの品質をスコア形式で計測する。

バグの元になる書き方からコードの複雑度まで様々な項目を  
1つのツールで解析でき、CIへの導入もしやすい。

## インストール・使用方法
`composer`を使用しているプロジェクトであればインストールは簡単。
```bash
composer require nunomaduro/phpinsights --dev
```
解析する場合はインストールされたバイナリを実行する。
```bash
./vendor/bin/phpinsights analyse [解析するディレクトリ・ファイル]
```

### テスト導入中に発生したエラー
`symfony/cache`のバージョンが関係するエラーに遭遇したため、  
場合によってはアップグレードが必要かもしれない。
```bash
composer require symfony/cache:6.0 --dev -W 
```

## 実行オプション
### インタラクションをしない
解析結果の表示時にユーザー入力を待つことがあるが、  
`-n`を指定することでこれを行わない。

解析結果を別ファイルに出力したい時などに有効。
```bash
./vendor/bin/phpinsights analyse -n > temp.txt
```

### 設定ファイルを読み込む
`-c`で解析時に参照する設定ファイルを指定する。
```bash
./vendor/bin/phpinsights analyse -c config.php
```

## 設定ファイル
`vendor/nunomaduro/phpinsights/stubs/config.php`が設定ファイルのテンプレートになっている。  
設定ファイルを作るときはこれをコピーすると便利。