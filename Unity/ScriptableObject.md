あるデータをまとめたコンテナのアセット。  
クラスとして作成するがGameObjectに直接アタッチできない。  

データをアセットとして保存し、それをコンポーネントに  
アタッチして使う形になる。

## 例
以下のようなScriptableObjectを作成し、  
利用する側のクラスにアタッチすることでスクリプト内からその値を使える。
```csharp
using UnityEngine;

// ScriptableObjectを継承させることで、  
// UnityのGUIからこのクラスのデータをアセットとして保存できるようになる
[CreateAssetMenu(fileName = "Data", menuName = "ScriptableObjects/HogeDataObject", order = 1)]
public class HogeDataObject : ScriptableObject 
{
	public Vector3 startPosition;
	public float moveSpeed;
}
```

```csharp
using UnityEngine;

public class HogeCharacter : MonoBehaviour
{
    // 上で定義した ScriptableObject のインスタンス
    [SerializeField]
    private HogeDataObject hogeData;
    
    private float moveSpeed;
    
    void Start()
    {
	    transform.position = hogeData.position;
	    moveSpeed = hogeData.moveSpeed;
    }
}
```

## 参考
<https://note.com/citronworld/n/n47965ddec2ec>  
<https://docs.unity3d.com/ja/2018.4/Manual/class-ScriptableObject.html>