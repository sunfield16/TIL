## Gizmo
Unityのエディター上に図形やアイコンを表示できるデバッグ機能。  
スクリプトに記載することで、かなり自由度の高い表示ができる。

主に「ゲーム画面上からは見えない要素」を見えるようにする目的で使われる。  
例としては下記。  
* 敵キャラクターのHP
* 敵キャラクターの移動予定・索敵範囲
* 各オブジェクトの当たり判定（選択していない状態でも見えるようにする）

## 書き方
基本は各スクリプト内で`OnDrawGizmos()`の内部に記述する。
`#if UNITY_EDITOR`で囲んでおくことで、デプロイ時に含まれることもない。
```csharp
#if UNITY_EDITOR
    void OnDrawGizmos()
    {
    
    }
#endif
```

```csharp
#if UNITY_EDITOR
    void OnDrawGizmos()
    {
        // 線などの色を指定する
        Gizmos.color = Color.blue;
        
        // 線分を表示
        Gizmos.DrawLine(transform.position, transform.position + Vector3.up * 5.0f);
        
        // 直線を表示
        Gizmos.DrawRay(new Ray(transform.position, Vector3.up));
        
        // 円、四角（塗りつぶし）を表示
        Gizmos.DrawSphere(transform.position, 5.0f);
        Gizmos.DrawCube(transform.position, Vector3.one);
        
        // 円、四角（ワイヤーフレーム）を表示
        Gizmos.DrawWireSphere(transform.position, 5.0f);
        Gizmos.DrawWireCube(transform.position, Vector3.one);
    }
#endif
```
