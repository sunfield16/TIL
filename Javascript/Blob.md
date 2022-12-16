## Blob
Blobは`Binary Large OBject`の略で、いわゆる「ファイル」を扱うためのオブジェクト。  
テキストやバイナリデータとして読み込む他、ダウンロードさせる際にも使える。

Blobという名前自体はデータベースのデータ型にもあり、  
画像や音声などのバイナリデータを扱う型として使われる。

## Blobを生成する
Blobの内容物とMIMEタイプを指定することで生成可能。
```javascript
const content = "hogehoge";
const mime = "plain/text";

// 内容物は配列で指定する
const blob = new Blob([ content ], {"type": mime});
```

### 例: Blobでjsonを扱う場合
```javascript
const jsonObject = {
    "test1": "hoge1",
    "test2": "hoge2"
};

// Blobを生成する時はjsonを文字列に変換して指定する必要がある
const blob = new Blob([ JSON.stringify(jsonObject) ], {"type": "application/json"});
```

## 中身の取得
### FileReader
```javascript
const fileReader = new FileReader();

// 読み込み完了時のコールバックを設定
fileReader.onload = function(e) 
{
    console.log(e.target.result);
};

// 実際に読み込んで中身を取得する
fileReader.readAsText(settingsFile);
```