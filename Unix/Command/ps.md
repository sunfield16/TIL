## psコマンド
現在OS上で動作しているプロセスを一覧で表示する。  
プロセスはLinux上での処理1つ1つであり、ps自体も実行すればプロセスの1つ。  
なので、psを実行した時はそれも一覧に表示される。

残っている不要なプロセスを確認したり、PCの動作が重い時に  
原因になっているプロセスを特定したり等用途は広い。

## 基本の使い方
```bash
ps [オプション]
```

psのオプションには、通常のコマンドでつける`-`や`--`が不要なものが多い。

## 表示関連オプション

オプション名 | 効果 
-----------|----------
 a         | 端末から実行しているプロセスを表示
 x         | 端末以外から実行しているプロセスを表示
 u         | CPUやメモリの使用量を表示
 r         | 実行中のプロセスを表示
 c         | 実行中のコマンドの名前を表示
 e         | コマンド名に加えて環境変数を表示
 l         | 実行時間等の詳細な情報を表示（`u`と同時指定不可）
 f         | プロセスを階層形式で表示

オプション指定は下記のように行う。
```bash
# a,u,xのオプションを指定してps実行
ps aux
```

## Stat
Statはpsコマンドによって確認できる、プロセスの状態。  
プロセスが実行されているか、スリープしているか等を確認できる。

### bashでの説明
表記   | 意味
------|----------
 `S`  | 割り込み可能なスリープ状態（ユーザー入力等のイベント完了待ち）
 `D`  | 割り込み不可能なスリープ状態（基本的には`IO`を行っている時）
 `R`  | 実行中、または実行待機中
 `T`  | 停止中
 `U`  | 割り込み不可能な待機状態
 `Z`  | 親プロセスとの関係が切れてしまった（ゾンビ）状態

### zshでの説明
表記   | 意味
------|----------
 `S`  | 約20秒未満のスリープ状態（割り込み可能）
 `I`  | 約20秒以上のスリープ状態（割り込み可能）
 `R`  | 実行待機中
 `T`  | 停止中
 `U`  | 割り込み不可能な待機状態
 `Z`  | 親プロセスとの関係が切れてしまった（ゾンビ）状態

↑に追加で、以下の表示がついていることもある。

表記   | 意味
------|----------
 `+`  | その制御端末でフォアグラウンドのプロセスグループにいる
 `s`  | セッションリーダーになっている
 `<`  | CPU優先度が高い
 `N`  | CPU優先度が低い

### Stat表示例
```
R+ ... フォアグラウンドで実行待機中（psコマンドも実行すると基本これになる）
```