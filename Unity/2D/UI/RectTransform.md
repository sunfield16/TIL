## 参考
[Unity公式](https://docs.unity3d.com/ja/2019.4/Manual/UIBasicLayout.html)

## RectTransform
Canvasに設置するUI関連のGameObjectに搭載されているコンポーネント。  
通常のTransformとは異なり、Canvas内での位置やスケールを扱う。

## RectTransformの座標
RectTransformでは、「1px = 1Unit」として扱われる。  
なので画面サイズが「800 x 600」の時にUIを真ん中に表示したい場合は、  
Canvas内で(400,300)の位置にUIを配置する必要がある。

## Anchor
親GameObjectのどこを基準に移動・スケーリングするかの設定。X,Yそれぞれの最大と最少を設定できる。  
主に親との位置関係を決めるのに使う。

※まだAnchorに対して言語化できるほどの理解がないので、参考URLを見つつさらに理解を深める。

## Pivot
画像の中で、回転やスケーリングの中心点を設定する。  
Anchorとはまた違った概念。

## RectTransformのParent
`RectTransform`の親オブジェクトを変更する場合、必ず`SetParent`を使うようにする必要あり。
```csharp
// こっちを呼ぶ
transform.SetParent(parentObject, false)

// これはダメ（警告が出る）
transform.parent = parentObject;
```
以下のような警告が出る。
```
Parent of RectTransform is being set with parent property.
Consider using the SetParent method instead, with the worldPositionStays argument set to false.
This will retain local orientation and scale rather than world orientation and scale, 
which can prevent common UI scaling issues.
```