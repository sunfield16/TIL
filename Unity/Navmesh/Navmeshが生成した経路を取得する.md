## Navmeshで自動で移動する場合
NavmeshAgentのプロパティに目標の場所を指定すると、  
Navmeshが生成した経路に合わせて自動で移動してくれる。
```csharp
NavmeshAgent _navmeshAgent = GetComponent<NavMeshAgent>();

void Start()
{
	_navmeshAgent.destination = new Vector3(10.0f, 0.0f, 10.0f);	
}
```
移動速度などもある程度設定できるが、  
自前での移動処理を使いたい場合などには向かない。

## Navmeshが生成した経路を取得する
NavmeshのシングルトンクラスでBake済みのNavmeshにアクセスでき、  
スタート地点とゴール地点を指定することで経路を取得できる。
```csharp
// あらかじめ経路探索の結果を入れるためのクラスを作っておく必要あり
NavmeshPath navmeshPath = new NavMeshPath();

Vector3 targetPosition = new Vector3(10.0f, 0.0f, 10.0f);
bool succeed = NavMesh.CalculatePath(transform.position, targetPosition, NavMesh.AllAreas, navmeshPath);
if(!succeed)
{
     Debug.LogError("calclate failed");
}
```
引数で指定した`NavmeshPath`にゴール地点に行くまでの経路が格納される。  
これを順番に辿る形で移動処理を組めば、  
NavmeshAgentを使わない形で移動させることができる。
```csharp
// ゴール地点に行くまでの経路（Vector3の配列）
Vector3 firstTarget = navmeshPath.corners[0]
```