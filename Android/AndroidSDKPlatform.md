<https://developer.android.com/tools/releases/platforms?hl=ja>

AndroidStudioのSDK Managerからダウンロードできる  
SDKパッケージ群。

## Android Platform Tools
各バージョン向けのアプリをコンパイルする時に必要になる。  
TargetSDKVersionの指定に合わせて必要といった感じ？

## System Image
特定のAPIレベルのエミュレータを実行する時に必要になる。  
追加でラベルが付いているが、それぞれ以下のような感じ。

* 各種アーキテクチャ: それぞれに対応したエミュレータが使える
	- ARM64 v8a, Intel x86, x86_64, etc...
* デバイス: それぞれに対応したエミュレータが使える
	- Wear OS, Google TV, etc...
* Google APIs: GooglePlay開発者サービスが使える
	- <https://developers.google.com/android/guides/overview?hl=ja>
* GooglePlay : GooglePlayストアをインストールしたエミュレータが使える
	- 課金確認などをしたい場合は必要

例えば、以下のような感じになる。

* `GooglePlay ARM64 v8a`: GooglePlayストアありの ARM64 v8a エミュレータ
* `Google TV Intel x86`: Google TV デバイスの Intel x86 エミュレータ（GooglePlayストアなし）