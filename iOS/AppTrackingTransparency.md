## 参考
iOS14でのIDFA取得  
<https://qiita.com/yofuru/items/213b88b85553631204e4>

## AppTrackingTransparency
AppTrackingTransparencyは、広告目的によるユーザーの端末データ(IDFA)取得の許可を  
ユーザーに求めるためのフレームワーク。

iOS14から、IDFAの取得にはこれによる許可リクエストが必須となっている。

## そもそもIDFAとは
IDFAは `Identifier For Advertising` の略で、主に広告目的で使用する端末固有のID。  
一般的には「トラッキングID」と呼ばれる。

各広告プラットフォーム(AppsFlyer, Tapjoy等)はこれを使用して、  
ユーザーに合った広告を表示したり、分析のためにアプリ内の行動追跡を行ったりする。

## ATTrackingManager
`ATTrackingManager`で下記を行うことが可能。

* 現在の許可状態を取得する
* 許可を求めるアラートを表示する

```objectivec
// import
#import <AppTrackingTransparency/AppTrackingTransparency.h>

// 現在の許可状態を取得する
ATTrackingManagerAuthorizationStatus status = [ATTrackingManager trackingAuthorizationStatus];

// 許可を求めるアラートを表示する
[ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status)
{

}];
```

### `ATTrackingManagerAuthorizationStatus`
`trackingAuthorizationStatus`で取得できる状態は下記の種類がある。

enum          | 内容
--------------|----------
Authorized    | 許可されている
Denied        | 不許可されている
Restricted    | 制限された
NotDetermined | 未確定

### `requestTrackingAuthorizationWithCompletionHandler`
許可を求めるアラートを表示した後、コールバックによって処理を行うことが可能。

```objectivec
[ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status)
{
    // コールバック処理
    switch (status)
    {
        case ATTrackingManagerAuthorizationStatusAuthorized:{
            // 許可された場合、各種広告プラットフォームのSDK初期化をする等の処理がここでできる
            NSLog(@"authorized");
        } break;
            
        case ATTrackingManagerAuthorizationStatusDenied:{
            NSLog(@"denied");
        } break;
            
        case ATTrackingManagerAuthorizationStatusRestricted:{
            NSLog(@"restricted");
        } break;
            
        case ATTrackingManagerAuthorizationStatusNotDetermined:{
            NSLog(@"notdetermined");
        } break;
            
        default:{ break; }
    }
}];
```