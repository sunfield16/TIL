# Android.mk
## 結局Android.mkって何？
* ビルド対象に含むソースやライブラリを指定するためのファイル
* ソースを下記のような「モジュール」の単位で区分できる
  - 静的ライブラリ
  - 共有ライブラリ
  - 実行可能ファイル
* 同じソースを複数のモジュールで使うことも可能

## Android.mkの基本の書き方
基本的には下記の手順で書いていく。

* 「LOCAL_PATH」の定義
* 各モジュールごとにビルド内容・方法の設定
  - ビルドするモジュール名の指定
  - ビルドするソースファイルの指定
  - ビルド内容・方法の設定
* 変数「CLEAR_VARS」の宣言

### 「LOCAL_PATH」の定義
最初に開発ツリー内のソースファイルの場所である変数  
「LOCAL_PATH」を定義する

``` makefile

# 「my-dir」 -> このmkファイルがあるディレクトリを取得する
#  makefileの関数として用意されている
LOCAL_PATH := $(call my-dir)
```

### 各モジュールごとのビルド内容・方法の設定
モジュールをビルドするには、あらかじめ指定されている  
`LOCAL_XXX`のような変数に設定を入れていき、最後に  
ビルド方法を設定する必要がある。

* ビルドするモジュールの名前を「LOCAL_MODULE」に指定する  

``` makefile
# モジュールの名前は一意である必要がある
# ここで指定した名前のファイルがビルド時に作られる
# 名前は接頭辞に「lib」がつけられる（既についてたらそのまま）
LOCAL_MODULE := hello-jni
```

* ビルドするソースファイルを指定していく（複数あったら空白で区切る）

``` makefile
LOCAL_SRC_FILES := hello-jni.c
```

* 最後に、ここまでで設定した`LOCAL_XXX`の情報を集めてビルド内容を決める

``` makefile
# ここで指定できる設定は下記の通り
# * BUILD_SHARED_LIBRARY
#   - 共有ライブラリをビルドする際に使う
#   - 「.so」ファイルが生成される
# * BUILD_STATIC_LIBRARY
#   - 静的ライブラリをビルドする際に使う
#   - これを使うと静的ライブラリを共有ライブラリのビルドに使える
#   - 「.a」ファイルが生成される
# * PREBUILT_SHARED_LIBRARY
#   - 事前にビルドされた共有ライブラリだけをソースで指定する時に使う
#   - LOCAL_SRC_FILESのファイルを含むことはできない
# * PREBUILT_STATIC_LIBRARY
#   - PREBUILT_SHARED_LIBRARYのSTATIC版
include $(BUILD_SHARED_LIBRARY)
```

これで1つのモジュールのビルド設定が完了する。

### 変数「CLEAR_VARS」の宣言
一部の変数を自動的にクリアしてくれる「CLEAR_VARS」を宣言する

``` makefile
include $(CLEAR_VARS)
```

* 「CLEAR_VARS」は`LOCAL_XXX`のようないくつかの変数を  
  自動的にクリアしてくれる
  - 「LOCAL_PATH」はクリアされない
* これを呼ばない場合、次のモジュールのビルド設定を作る時に  
  前の`LOCAL_XXX`の設定が入ってしまう
  - なので各モジュールの設定を作るごとに呼ぶ必要あり

## mkを支える変数・マクロたち
Android.mkにはデフォルトで用意されている変数やマクロがたくさんある。  
下記のような種類に分けられる。

Android.mk内では自分で変数を定義することもできるが、下記にある名前は使えないので注意。  
公式では変数の頭に「MY_」のような接頭辞をつけることを推奨している。

* NDKで定義されたinclude用変数
  - `CLEAR_VARS`
  - `BUILD_SHARED_LIBRARY`
  - `BUILD_STATIC_LIBRARY`
  - `PREBUILT_SHARED_LIBRARY`
  - `PREBUILT_STATIC_LIBRARY`

* ターゲット情報変数
  - `TARGET_ARCH`
  - `TARGET_PLATFORM`
  - `TARGET_ARCH_ABI`
  - `TARGET_ABI`

* モジュール設定変数
  - `LOCAL_PATH`
  - `LOCAL_MODULE`
  - `LOCAL_MODULE_FILENAME`
  - `LOCAL_SRC_FILES`
  - `LOCAL_CPP_EXTENSION`
  - `LOCAL_CPP_FEATURES`
  - `LOCAL_C_INCLUDES`
  - `LOCAL_CFLAGS`
  - `LOCAL_CPPFLAGS`
  - `LOCAL_STATIC_LIBRARIES`
  - `LOCAL_SHARED_LIBRARIES`
  - `LOCAL_WHOLE_STATIC_LIBRARIES`
  - `LOCAL_LDLIBS`
  - `LOCAL_LDFLAGS`
  - `LOCAL_ALLOW_UNDEFINED_SYMBOLS`
  - `LOCAL_ARM_MODE`
  - `LOCAL_ARM_NEON`
  - `LOCAL_DISABLE_FORMAT_STRING_CHECKS`
  - `LOCAL_EXPORT_CFLAGS`
  - `LOCAL_EXPORT_CPPFLAGS`
  - `LOCAL_EXPORT_C_INCLUDES`
  - `LOCAL_EXPORT_LDFLAGS`
  - `LOCAL_EXPORT_LDLIBS`
  - `LOCAL_SHORT_COMMANDS`
  - `LOCAL_THIN_ARCHIVE`
  - `LOCAL_FILTER_ASM`

* NDKの関数マクロ
  - `my-dir`
  - `all-subdir-makefiles`
  - `this-makefile`
  - `parent-makefile`
  - `grand-parent-makefile`
  - `import-module`

