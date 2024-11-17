<https://qiita.com/toRisouP/items/86fea641982e6e16dac6#unirxtriggers%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA>

UniRxで、Unityの基本的なコールバックを`IObservable`として取得する機能。  
基本的には`XxxAsObservable`のようなメソッドが拡張で追加されている。

* Update
* FixedUpdate
* OnTriggerEnter
* OnTriggerExit

をはじめとしたほぼ全てのコールバックイベントに対応。  
究極的には、Updateなどに書いていた処理を  
**全てAwakeやStartにまとめて記述**してしまうことができる。

Destroyされたときにも`OnComplete`は自動で発行されるので寿命も意識しなくていい。


## Triggersによるメリット
<https://qiita.com/toRisouP/items/30c576c7b0a99f41fb87#2update%E3%82%92%E3%82%B9%E3%83%88%E3%83%AA%E3%83%BC%E3%83%A0%E3%81%AB%E5%A4%89%E6%8F%9B%E3%81%99%E3%82%8B%E3%83%A1%E3%83%AA%E3%83%83%E3%83%88>

Updateなどを`IObservable`で扱うメリットは以下のようなものがあるとされる。

* オペレータでロジックを記述できる
* ロジックの処理単位がわかりやすい

### オペレータでロジックを記述できる
例えば、シューティングゲームでよくある  
「ボタンを押している間一定間隔で攻撃する」というような処理。

フレーム管理などが少し面倒だが、これをオペレータで制御すると  
宣言的に書けて簡潔になる。

```csharp
void Start()
{
	// UpdateをIObservableに変換
	this.UpdateAsObservable()
		// Zキーを押してる時
		.Where(_ => Input.GetKey(KeyCode.Z))
		// 最後に実行してから0.25秒OnNextを遮断（つまり一定間隔で実行される）
		.ThrottleFirst(TimeSpan.FromSeconds(0.25f))
		// イベントが発行されたら攻撃処理
		.Subscribe(_ => Attack());
}

void Attack()
{
	// ここに攻撃処理
}
```

### ロジックの処理単位がわかりやすい
UpdateAsObservableにも、もちろん複数Subscribeを行うことができる。  
つまり、「移動」「ジャンプ」「攻撃」など、  
それぞれのロジックを分割・整理して記述できる。

しかも、変数のスコープもストリーム内に閉じやすく  
明確になりやすい。