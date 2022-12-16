## curl
HTTPをはじめとした様々なプロトコルでリクエストを送信するコマンド。  

* 各種APIへのHTTPリクエスト
* POSTでのパラメータ指定の確認
 
など、気軽にURL指定でAPIを実行したい場合などは、  
curlを使うことで楽に進められる。

## 基本の使い方
オプションの後にURLを書いてもいいし、逆でも大丈夫。
```bash
curl [オプション/URL]
```

### 使用例
ローカルにサーバーを建ててあるとして、HTTPでGETリクエストを送る場合は以下のようになる。
```bash
curl "http://localhost:8080/index.html"

# 出力例
<!DOCTYPE html>
<html lang="ja">
	<head>
		<meta charset="UTF-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Document</title>
	</head>
	<body>
		Hello World
	</body>
</html>
```

## リクエストのタイプを指定
`-X`でリクエストのタイプを指定できる。
POST, PUT, DELETEなどが指定可能。

パラメータは`-d`で指定する。
```php
# test.php
# 単純にリクエストで来たパラメータを返すだけ
<?php
$hoge = $_REQUEST["hoge"];
$fuga = $_REQUEST["fuga"];

echo json_encode(["hoge" => $hoge, "fuga" => $fuga]);
```

```bash
# POSTでリクエストを送る
curl -X POST "http://localhost:8080/test.php" -d "hoge=1&fuga=2"
{"hoge":"1","fuga":"2"}
```

## 出力先を別ファイルに保存
`-o`で出力先のファイルを指定できる。  
`-O`にするとURLのファイル名で現在のディレクトリに保存する。
```bash
# test.txtにindex.htmlへのリクエストの内容が保存される
curl -o "./test.txt" "http://localhost:8080/index.html"

# URLのファイル名（index.html）で保存
curl -O "http://localhost:8080/index.html"
```

## 画面出力を制御する
`-s`を指定することで画面への出力を非表示にできる。  
（ただしエラーメッセージも出なくなってしまう）

`-S`を指定するとエラーメッセージの出力が可能。  
基本的には`-sS`のように両方を指定する形になる。
```bash
# ポートが違っていてアクセスできなかったとしても、-sがあるので何も出ない
curl -s "http://localhost:8081/index.html"

# -Sを一緒に指定すると、エラーのみ出る
curl -sS "http://localhost:8081/index.html"
curl: (7) Failed to connect to localhost port 8081: Connection refused
```

## ヘッダーを含めた出力
curlではHTTPのリクエスト・レスポンスヘッダーも確認可能。

* `-I` ... レスポンスヘッダーを出力
* `-i` ... レスポンスヘッダー・ボディの両方を出力
* `-v` ... リクエストもレスポンスも全部出力（verbose）

```bash
# レスポンスのヘッダーだけが出る
# -iを指定した場合はこの下にレスポンスボディも出る
curl -I "http://localhost:8081/index.html"
HTTP/1.1 200 OK
**Host**: localhost:8080
**Date**: Wed, 02 Nov 2022 09:48:12 GMT
**Connection**: close
**Content-Type**: text/html; charset=UTF-8
**Content-Length**: 310

# -vでリクエストのヘッダーも出力
curl -v "http://localhost:8080/index.html"
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8080 (#0)
> GET /index.html HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Host: localhost:8080
< Date: Wed, 02 Nov 2022 09:50:01 GMT
~~~ 以下省略 ~~~
```