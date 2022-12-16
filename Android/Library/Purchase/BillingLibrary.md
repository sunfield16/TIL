## 参考資料
[Google Play Billing Library をアプリに統合する](https://developer.android.com/google/play/billing/integrate)

## BillingLibrary
BillingLibraryはGoogleが公式で提供している課金処理ライブラリ。  
GooglePlayで配信するAndroidアプリは基本的にこれを使って課金部分の実装を行うことになる。

## BillingClientの生成
BillingLibraryを使う際はまず`BillingClient`を生成する。  
BillingClientはGooglePlayとの通信を行う様々な処理を扱うクラス。

基本的にはこのクラスを使って課金アイテム情報の取得や購入を行うことになる。  
原則としてBillingClientは1つだけ生成するため、メンバー変数に保持するのがベスト。
```java
// 課金処理用のクラスを用意
public class StoreController
{
    // Builderを使ってBillingClientを初期化する
    private BillingClient _billingClient = BillingClient.newBuilder(activity)
        .enablePendingPurchases()
        .build();
```

## GooglePlayへの接続
GooglePlayへの接続は`startConnection`で行う。  
コールバックで成否の確認や接続が切れた場合の処理が記述可能。

この処理は非同期なので、アプリ側では通信待機の表示を出す等の対応が必要。
```java
_billingClient.startConnection(new BillingClientStateListener() {
    @Override
    public void onBillingSetupFinished(BillingResult billingResult) {
        // 接続完了した時のコールバック
        if (billingResult.getResponseCode() ==  BillingResponseCode.OK) {

        }
    }
    @Override
    public void onBillingServiceDisconnected() {
        // 通信が切断された時のコールバック
        // 基本的には再接続等で通信の維持をする
    }
});
```

## アイテム情報の取得
取得したいアイテムのリストと種類を指定することで  
それらのアイテム情報を取得可能。

この処理も非同期なので注意が必要。
```java
// アイテム情報取得のためのデータ構造を生成
// ProductTypeは取得したいアイテムの種類で、
// INAPP(1回限りの購入) か SUBS(定期購入)
ArrayList<QueryProductDetailsParams.Product> productList = new ArrayList<QueryProductDetailsParams.Product>();
productList.add(QueryProductDetailsParams.Product.newBuilder()  
        .setProductType(BillingClient.ProductType.INAPP)  
        .setProductId("hoge_stone_1")  
        .build());

QueryProductDetailsParams.Builder params = QueryProductDetailsParams.newBuilder()  
        .setProductList(productList)
        .build();

// Product情報の取得
_billingClient.queryProductDetailsAsync(params, 
	new ProductDetailsResponseListener() 
	{        
		public void onProductDetailsResponse(BillingResult billingResult,                List<ProductDetails> productDetailsList) 
		{
			// ここでアイテムの情報を取得したりする
		}    
	}  
)
```

### ProductDetailsの中身
ProductDetailsにはアイテムの価格やストア上での説明文などが入っている。

```java
// アイテムのID（プロダクトコード）
productDetails.getProductId();
// アイテムの説明文
productDetails.getDescription();

// 1回限りの購入アイテムの情報取得
// （専用の構造体にまとまってる）
ProductDetails.OneTimePurchaseOfferDetails oneTime = productDetails.getOneTimePurchaseOfferDetails();

// 通貨記号を含む価格(￥2,200など)
oneTime.getFormattedPrice();
// マイクロ単位の価格(2,200円の場合、2200000000)
oneTime.getPriceAmountMicros();
// ISO 4217準拠の通貨単位を返す(JPYなど)
oneTime.getPriceCurrencyCode();
```

## 購入フローを開始する
実際にアイテムを購入する場合は`launchBillingFlow`を実行する。  
購入にはアイテム情報が必要なため、事前に取得しておかないといけない。

`BillingFlowParams.ProductDetailsParams`のリストを渡す形式になっており、  
購入するアイテムは複数指定が可能。
```java
// 購入する商品の情報を指定する 
BillingFlowParams.ProductDetailsParams product = BillingFlowParams.ProductDetailsParams.newBuilder()
                .setProductDetails("hoge_stone_1")
                .build();

List<BillingFlowParams.ProductDetailsParams> productDetails = new ArrayList<BillingFlowParams.ProductDetailsParams>();
productDetails.add(product);
  
// 商品を指定して購入フローの開始  
BillingFlowParams billingFlowParams = BillingFlowParams.newBuilder()  
        .setProductDetailsParamsList(productDetails)  
        .build();  

// 戻り値で「購入フローの起動に成功したか」が取得できる
// （購入自体の成否確認はコールバックで行う）
int responseCode = billingClient.launchBillingFlow(activity, billingFlowParams).getResponseCode();
```

### 購入の結果を受け取る
BillingClientには購入状態に関する情報を受け取るためのリスナーを設定できる。  
これによって購入の結果や購入したアイテムの情報を取得したりする。
```java
    // 購入状態を受け取るリスナー
    private PurchasesUpdatedListener purchasesUpdatedListener = new PurchasesUpdatedListener() {
        @Override
        public void onPurchasesUpdated(BillingResult billingResult, List<Purchase> purchases) {
            // 
        }
    };

    // リスナーはBillingClientの初期化時に設定する
    private BillingClient _billingClient = BillingClient.newBuilder(activity)
            .setListener(purchasesUpdatedListener)
            .enablePendingPurchases()
            .build();
```

### Purchaseの中身
Purchaseにはその購入に関する各種情報が入っている。  

 メソッド              | 内容
----------------------|----------
 getOrderId           | その支払いのオーダーID
 getProductId         | 購入したアイテムのID
 getPurchaseState     | PENDING(保留)、PURCHASED(支払い完了)のどちらか
 getPurchaseTime      | 購入完了した時間(エポック時間)
 getPurchaseToken     | 購入トークンの文字列
 getSignature         | ストアに登録した秘密鍵で署名された、購入データの署名文字列
 isAcknowledged       | サブスクリプション等で、購入が承認されているかどうかを返す

## 購入を処理する
アイテムを購入した後は、アプリからGooglePlayに  
「アイテムの内容をユーザーに付与した」ことを伝える必要がある。  
（=購入を処理する）

1回限りの購入アイテムでは、購入を処理するまでは  
同じアイテムを購入できない。

```java
// 例: 購入状態を受け取るコールバック内で購入を処理する
@Override
public void onPurchasesUpdated(BillingResult billingResult, List<Purchase> purchases) {
    Purchase purchase = purchases[0];

    // 各購入ごとのトークンを指定して購入処理用のパラメータを生成
    ConsumeParams consumeParams =
        ConsumeParams.newBuilder()
            .setPurchaseToken(purchase.getPurchaseToken())
            .build();

    // 購入処理の結果を受け取るリスナーの作成
    ConsumeResponseListener listener = new ConsumeResponseListener() {
        @Override
        public void onConsumeResponse(BillingResult billingResult, String purchaseToken) {
            if (billingResult.getResponseCode() == BillingResponseCode.OK) {
                
            }
        }
    };

    billingClient.consumeAsync(consumeParams, listener);
}
```

## 購入の確認
「コンビニ払い」など、支払いの方法によっては即時的に購入が完了しないこともある。  
こういった支払い方法では、支払いが完了するまでは  
利用権を付与しないようにする必要がある。  
（タダで利用権を得られてしまう状況が発生するため）

PurchasesUpdatedListenerで購入情報を受け取った時には、  
必ず購入の状態を見て支払いが完了したことを確認することが重要。

```java
public void onPurchasesUpdated(BillingResult billingResult, List<Purchase> purchases) 
{
    for (final Purchase purchase : purchases) {
        if (purchase.getPurchaseState() == Purchase.PurchaseState.PURCHASED) {
            // 支払いが完了(PURCHASED)の場合のみ利用権を付与する
        }
    }
}
```

また、実際の支払いが完了しているかどうかを判断するために、  
購入の情報を取得するメソッドも用意されている。

```java
// `inapp`で一回限りの購入、`subs`で定期購入の購入情報を取得
Purchase.PurchasesResult purchasesResult = _billingClient.queryPurchases("inapp");

int responseCode = purchasesResult.getResponseCode();
if (responseCode == BillingClient.BillingResponseCode.OK) {
    List<Purchase> purchases = purchasesResult.getPurchasesList();
    for (final Purchase purchase : purchases) {
        if (purchase.getPurchaseState() == Purchase.PurchaseState.PURCHASED) {
            // 支払いが完了(PURCHASED)の場合のみ利用権を付与する
        }
    }
}
```