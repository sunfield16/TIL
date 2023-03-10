## crontab
crontabは、コマンドを指定した時間に実行するためのスケジュール管理コマンド。  
内部で専用のファイルにコマンドを記録し、指定した時間になると自動でそのコマンドを実行する。

1回きりの実行だけではなく、指定した時間の定期実行も可能。  
例えば、「毎朝8時に実行したい」といった場合もcrontabに登録することで忘れずに実行してくれる。  
何らかのデータ監視・通知を行う場合などに有効。

慣習的に`cron`（クーロン）と呼ばれる。

## 基本の使い方
```bash
# 登録時
crontab [実行パターン] [実行するコマンド]

# 確認・編集時
crontab [オプション]
```

## 実行パターン
左から順に、「分」「時」「日」「月」「曜日」の指定を行う。  
`*`を指定すると、その単位で「毎回」行われる。（詳細は後述）

```bash
# 例

# 毎分実行
* * * * *

# 毎日8時ぴったりに実行
# （8時00分）
0 8 * * *

# 毎年2月3日に実行
0 0 2 3 *
```

実際に`crontab`を使う場合は下記のように指定する。
```bash
# 毎日8時ぴったりに「hogehoge.sh」を実行する
crontab 0 8 * * * hogehoge.sh
```

### 特殊書式
```bash
* -> 任意の値を表す（その単位で「毎回」行う）
, -> 単位内での複数指定（「6時と12時」など）
- -> 範囲での指定（「10時から15時まで」など）
/ -> 一定刻みの指定（「10時から3時間ごと」など）
```

```bash
# 例

# 毎日9時と21時に実行
0 9,21 * * *

# 毎日8時から19時まで毎時間実行
0 8-19 * * *

# 3日ごとに実行
0 0 */3 * *

# 毎日9時から14時、15時から21時まで毎時間実行
0 9-14,15-21 * * *
```

## オプション
```bash
-l -> 登録されているcrontabを確認する
-e -> 登録済みのcrontabの内容を編集する
-r -> crontabの内容を削除する
```