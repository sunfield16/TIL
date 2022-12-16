## Entitlements
Entitlementsは、iOSやMacのアプリ内で 
Appleの提供する各種機能(Capabilities)やサービスを使うことができる「資格」を表すファイル。  
-> 「このアプリは○○と××の機能が使えます」を指定するイメージ

実体は「plist」で、キーと値のペアによって記載する。  
Xcode上から操作も可能。

## Capabilities
Appleの提供する各種機能を表す。  
Entitlementsに記載することで使用可能。

### 例
* In-App Purchase
  - アプリ内課金ができる
* PushNotifications
  - 外部からリモートによる「Push通知」を送れる
* Associated Domain
  - Webで特定のURLにアクセスした場合に、  
    このアプリを直接開けるようになる
  - URLはEntitlementsで指定する
* Sign In with Apple
  - 「AppleID」によるログイン機能を使える

## Provisioning Profileでの制限
Entitlementsに指定すればなんでも使えるわけではなく、  
Provisioning Profileに明示されているものでないと使えない。