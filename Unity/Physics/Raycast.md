## RayCast
Scene内のある位置から`Ray`（直線）を伸ばして、Scene内の何かにぶつかるかどうかを判定する機能。  
ぶつかったGameObjectの内容や、ぶつかった位置を取得できる。  
3Dシューティングで銃弾が当たったかどうかの判定や、NPCに話しかける判定をするとき等、  
用途は多岐にわたる。

## 使用方法
### 2D
```csharp
// 発射位置
Vector2 origin = _rigidbody.position;
// Rayを伸ばす方向
Vector2 direction = Vector2.up;
// Rayの長さ（指定しない場合は無限に伸びる）
float maxDistance = 50.0f;
// ぶつかった判定をするレイヤー（指定しない場合はどのレイヤーにもぶつかる）
int layerMask = LayerMask.GetMask("Enemy");

RaycastHit2D hit = Physics2D.Raycast(origin, direction, maxDistance, layerMask);
if(hit.collider != null)
{
  Debug.Log("Ray hit: " + hit.collider);
}
```

### 3D
```csharp
// 発射位置
Vector3 origin = _rigidbody.position;
// Rayを伸ばす方向
Vector3 direction = Vector3.forward;
// Rayの長さ（指定しない場合は無限に伸びる）
float maxDistance = 50.0f;
// ぶつかった判定をするレイヤー（指定しない場合はどのレイヤーにもぶつかる）
int layerMask = LayerMask.GetMask("Enemy");

// Raycastの結果を保存するクラス
RaycastHit hit;
if (Physics.Raycast(origin, direction, out hit, maxDistance, layerMask))
{
  Debug.Log("Ray hit: " + hit.collider);
}
```
