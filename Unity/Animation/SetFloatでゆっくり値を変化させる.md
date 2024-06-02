## `Animator.SetFloat`でゆっくり値を変化させる
`SetFloat`の第3引数以降を指定することで、  
指定した値にゆっくり遷移させることができる。

「指定する値はほぼ固定だけど一気に変えたくない」といった場合に有効。  
```csharp
private float _animationDampTime;

void Update()
{
	// _animationDampTimeには変化しきるまでの時間を指定
	// 第4引数は基本的にdeltaTimeにする
	_animator.SetFloat("Speed", 2.0f, _animationDampTime, Time.deltaTime);
}
```
ゴール地点まで移動するのが目的のアクションゲームなどで、  
「ゴール時には操作は受け付けないけど、急にピタッと止まるんじゃなくゆっくり止めたい」  
みたいな場合などが考えられる。