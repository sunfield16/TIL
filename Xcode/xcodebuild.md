## xcodebuild
iOS向けのアプリをビルドする際はだいたいXcodeを起動して行うことになると思う。

これをターミナルから行えるのが「`xcodebuild`」である。  
Xcodeのインストール時に付属してくる。

## 基本的な使い方
「`-h`」でパラメータの説明が確認可能。

``` bash
xcodebuild -destination generic/platform=iOS \
			 -project '/hoge/hogepro.xcodeproj' \
			 -scheme 'hogepro-test' \
			 -configuration 'Debug' \
			 build
```

パラメータに`buildaction`を指定することでビルドの種類などを決められる。

* build → 通常のビルド
* clean → クリーンビルド
* archive → アーカイブ

## パラメータ
### `-project`
ビルドするプロジェクト（`.xcodeproj`）をパスで指定する

### `-destination`
アプリのインストール先を設定する（[項目名]=[パラメータ(カンマ区切り)]）

* 項目名 -> 設定する対象を表す。下記のどちらかを指定する
  - `platform` → 対象の機種（iOS, Mac, Simulatorなど）
  - `name` → 具体的な名前（「iPhone6」など） 
* パラメータ -> 項目に設定したい内容を記載する

また、「iOS全部」とかを指定する場合、項目名に「`generic/`」をつけることで全体を表せる。  
`generic/platform=iOS`とすれば「iOS全部」になる。  
CI/CDツール等でビルドを行う場合に有効。

### `-scheme`
ビルドターゲット名を指定する。  
（ビルドターゲットはXcode上では「Edit Scheme」で作成する）

### `-configuration`
デバッグビルドやリリースビルド等の指定を行う。  
（`Debug`や`Release`など）

### `-archivePath`
`archive`を指定する場合、`.xcarchive`が出力されるパスを指定する。