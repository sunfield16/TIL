## 衝突検知
Unityで衝突時に処理を行いたい場合、専用の組み込みメソッドをスクリプトに用意することで実現できる。  
もちろん、衝突検知のためにはColliderをそのGameObjectに追加しておく必要あり。

## 衝突した時の処理
衝突した瞬間だけ処理を行う。  
その後ぶつかり続けている場合は呼ばれない。

```csharp
void OnCollisionEnter2D(Collision2D other)
{

}
```
