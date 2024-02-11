https://qiita.com/toRisouP/items/86fea641982e6e16dac6#reactiveproperty%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA

普通の「変数」にSubjectの機能を追加したもの。  
変数の値を書き換えるとOnNextが発行される。

例えばHPをReactivePropertyにすると、HPが減ったのを検知して  
HPゲージに即時反映といったことができる。

```csharp
var hp = new ReactiveProperty<int>(10);
hp.Subscribe(x => Debug.Log(x));

// 値の変更はValueを介する
hp.Value = 20;
```

## コレクションを扱う
コレクションをReactivePropertyとして扱う場合、それぞれ専用のクラスを使う。

* `ReactiveCollection` ... `List<T>`
* `ReactiveDictionary` ... `Dictionary<T>`

こっちは要素の追加や削除、要素の上書きなどでOnNextが発行される。

## インスペクター上で扱える変数をReactivePropertyにする
`SerializeField`などでインスペクター上に公開する変数も、ReactivePropertyとして扱える。  
ただしその場合はそれぞれ専用のクラスを使う必要あり。

```csharp
// ReactiveProperty<int> の代わりに IntReactiveProperty を使う
private IntReactiveProperty _hp = new IntReactiveProperty(100);
```

## 読み取り専用で公開する
ReactivePropertyをそのまま外部に公開すると外から変更できてしまう。  
外側から変更されたくない場合は`IReadOnlyReactiveProperty`として公開する。
```csharp
public class HogeHoge : MonoBehavior
{
	private readonly IntReactiveProperty _hp = new IntReactiveProperty(100);

	// 読み取り専用で公開する。外側からはSubscribeで変更を検知する
	public IReadOnlyReactiveProperty<int> HP => _hp;
}
```