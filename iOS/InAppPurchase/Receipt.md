## 参考
https://developer.apple.com/jp/documentation/storekit/in-app_purchase/validating_receipts_with_the_app_store/

## Receipt
Appleの証明書で署名された、課金アイテム購入情報を扱う暗号化ファイル。  
iOSアプリで課金アイテムを購入するとアプリ側にReceiptが返却される。

基本的にはサーバーサイドに送信し、Receiptを使って  
その購入が正当であることを確認する。


## 中身を取得する
Appleが提供している`verifyReceipt`を使って、Receiptの中身を取得できる。

### Receiptの中身
中身はjsonで、以下のような形式になっている。
```json
{
	"receipt": 
	{
		"receipt_type": "ProductionSandbox",
		"adam_id": 0,
		"app_item_id": 0,
		"bundle_id": "app.hogehoge.bundle",
		"application_version": "1.0.1.1",
		"download_id": 0,
		"version_external_identifier": 0,
		"receipt_creation_date": "2022-09-27 07:03:23 Etc\/GMT",
		"receipt_creation_date_ms": "1664262203000",
		"receipt_creation_date_pst": "2022-09-27 00:03:23 America\/Los_Angeles",
		"request_date": "2022-09-27 07:03:29 Etc\/GMT",
		"request_date_ms": "1664262209487",
		"request_date_pst": "2022-09-27 00:03:29 America\/Los_Angeles",
		"original_purchase_date": "2013-08-01 07:00:00 Etc\/GMT",
		"original_purchase_date_ms": "1375340400000",
		"original_purchase_date_pst": "2013-08-01 00:00:00 America\/Los_Angeles",
		"original_application_version": "1.0",
		"in_app": 
		[
			{
			"quantity": "1",
			"product_id": "app.hogehoge.product1",
			"transaction_id": "xxxxxxxxxxxxxxxx",
			"original_transaction_id": "xxxxxxxxxxxxxxxx",
			"purchase_date": "2021-06-29 03:19:32 Etc\/GMT",
			"purchase_date_ms": "1624936772000",
			"purchase_date_pst": "2021-06-28 20:19:32 America\/Los_Angeles",
			"original_purchase_date": "2021-06-29 03:19:32 Etc\/GMT",
			"original_purchase_date_ms": "1624936772000",
			"original_purchase_date_pst": "2021-06-28 20:19:32 America\/Los_Angeles",
			"is_trial_period": "false",
			"in_app_ownership_type": "PURCHASED"
			},
			{
			"quantity": "1",
			"product_id": "app.hogehoge.product5",
			"transaction_id": "xxxxxxxxxxxxxxxx",
			"original_transaction_id": "xxxxxxxxxxxxxxxx",
			"purchase_date": "2022-09-27 07:03:22 Etc\/GMT",
			"purchase_date_ms": "1664262202000",
			"purchase_date_pst": "2022-09-27 00:03:22 America\/Los_Angeles",
			"original_purchase_date": "2022-09-27 07:03:22 Etc\/GMT",
			"original_purchase_date_ms": "1664262202000",
			"original_purchase_date_pst": "2022-09-27 00:03:22 America\/Los_Angeles",
			"is_trial_period": "false",
			"in_app_ownership_type": "PURCHASED"
			},
		]
	},
	"environment": "Sandbox",
	"status": 0
}
```