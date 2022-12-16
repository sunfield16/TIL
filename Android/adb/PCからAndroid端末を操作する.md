## adb経由でAndroid端末を操作する
PCにAndroid端末を接続している時は`adb shell input`で端末を操作できる。

```bash
adb shell input [操作] [引数]
```

## 指定した位置をタッチ
端末内の指定した座標をタッチする。  
座標は左上が原点で右下が+方向。

端末によって画面サイズは異なるため、UIの自動テストなどで使う場合は注意が必要。
```bash
adb shell input tap [x座標] [y座標]

# 例: (300, 500)の位置をタッチする
adb shell input tap 300, 500
```

## 指定したテキストを入力
入力欄にフォーカスがある状態で実行すると、文字列の通りにキーボードを打ち込んでいく。

マルチバイト文字は入力できないため、基本的には  
メールアドレスやパスワードの入力に使うことになる。
```bash
adb shell input text [文字列]

# 例:キーボードで「hogehoge@fugafuga.ne.jp」を入力する
adb shell input text hogehoge@fugafuga.ne.jp
```