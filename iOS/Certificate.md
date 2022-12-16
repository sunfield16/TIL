## 開発証明書
AppleDeveloperの管理画面で作成する、 **「自分はこのアカウントでアプリを開発してます」** を証明するファイル。  
これをMacのキーチェーンに登録することで、  
そのアカウントに紐づいたアプリが開発できるようになる。

## AppID
開発しているアプリを示す固有のID。  
例としては下記のような感じ。
```
AB23K7TM5B.jp.ne.hogecorp.fugaapp
```

AppIDは下記からなる。

* AppID Prefix
  - AppIDの前半部分(上の例では`AB23K7TM5B`)
  - デフォルトでは「TeamID」が割り当てられる
 
* AppID Suffix
  - AppIDの後半部分(上の例では`jp.ne.hogecorp.fugaapp`)

### AppID Suffixについて
これも2つに分けられる。
* Explicit App ID
  - アプリごとの固有のIDで、BundleIDと同じになる。  
    配布する場合はこれを使う。
* Wildcard App ID
  - 複数のアプリに使える汎用のID。

## BundleID
アプリを識別するためのID。AppIDからPrefixを取り除いた部分。

## TeamID
開発チームを表すID。Appleによって一意なIDが割り振られる。

## UDID
iOSの端末ごとに異なる固有のID。  
主にデバッグで使う端末を識別するのに使用する。

## Provisioning Profile
下記の内容が全て紐づいたファイル。

* AppID
* 開発証明書
* UDID

デバッグ用の端末に開発中のアプリをインストールしたり、  
アプリを申請する時に必要になる。