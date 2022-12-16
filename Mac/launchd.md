# launchdによる定期実行
## 参考
[launchdで定期的にスクリプトを実行](https://qiita.com/rsahara/items/7d37a4cb6c73329d4683)

## launchdとは
`launchd`は、MacOSで用意されているスクリプト実行機能。  
コマンドやタイミングを「ジョブ」として設定することで、  
それをlaunchdが定期的に実行してくれる。

Unix系のOSには同様の仕組みとして「`crontab`」が存在するが、  
MacOSではこれよりも`launchd`を使うことが推奨されている。

## 種類
* エージェント
* デーモン

の2種類が存在する。

### エージェント
ユーザーがログインしているときに実行できる。  
誰もPCにログインしてない場合は実行されない。

エージェントで設定する場合はユーザー単位で作成する。

### デーモン
誰もログインしてない場合でも実行できる。  
こちらはユーザーが関係ないため、専用の場所に1つだけ作成する。

## 設定方法
実行するジョブの設定は`.plist`で記述する。

### 設定例
`/path/to/file.php`を「月曜日の10時05分」に実行するジョブの設定例
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>hogehoge.com.test.launch</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/php</string>
        <string>/path/to/file.php</string>
    </array>
    <key>StartCalendarInterval</key>
    <array>
        <dict>
            <key>Weekday</key>
            <integer>1</integer>
            <key>Hour</key>
            <integer>10</integer>
            <key>Minute</key>
            <integer>5</integer>
        </dict>
    </array>
</dict>
</plist>
```

## 必須項目
### `Label`
ジョブの名前。基本的にはplistのファイル名と同じにする。

### `ProgramArguments`
実行するコマンドの内容を配列で記載する。  
基本的には1つ目の要素にコマンド、2つ目以降の要素にパラメータを入れることになる。

## オプション
### `UserName`
コマンドを実行するユーザーを指定する。  
エージェントの場合はログイン中のユーザー、  
デーモンの場合はrootがデフォルトになる。

### `StartInterval`
コマンドを実行する間隔を秒単位で指定する。  
頻繁に実行する定期実行ジョブのほか、20秒などで登録することでジョブ登録後の動作確認にも使える。

### `StartCalendarInterval`
コマンドを実行するタイミングを指定する（`StartInterval`との併用はできない）。  
これでcronと同じような時間指定の実行が可能。

また、「毎日10時と15時と20時に実行」のような複数指定もできる。

パラメータ | 内容
---------|----------
 Weekday | 曜日(1が月曜日、7が日曜日)
 Month | 月
 Day | 日
 Hour | 時
 Minute | 分 


## ジョブの登録・解除
作成したジョブ(`.plist`)を指定して、下記のコマンドで登録・解除ができる。
```bash
# 登録
launchctl load /path/to/file.plist

# 解除
launchctl unload /path/to/file.plist
```

どのパスに置いてあっても登録はできるが、ジョブ置き場として下記が  
用意されているのでそこに配置してから登録するのが良い。
```bash
# デーモン
/Library/LaunchDaemons/

# エージェント
[各ユーザーのホームディレクトリ]/Library/LaunchAgents/
```