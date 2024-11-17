# 概要
Unityで開発をしていると出くわしがちな  
アンチパターンと、その対処方法の例を紹介した資料。

# 参考資料
アンチパターンから学ぶUnityの使い方  
<https://learning.unity3d.jp/4159/>

# Public変数
## 問題点
* MonoBehaviourを継承したクラスでは、  
  Public変数の内容をInspector上から編集できる
  - そのデータがSerializeの対象になる
  - 当然、意図しない変更がされる可能性がある
* そもそも外部のクラスから値を変更できてしまう
  - 値の変更を管理しづらく、設計としては非常に危険
  - 必要な場合もあるが、可能な限り避けなければならない

## 対処法
* 可能な限り`[SerializeField]`を使う
  - publicにしなくてもSerializeの対象になる
  - Inspector上から編集できるのはそのまま
* Public変数ではなく、Setterとしてメソッドを公開する
  - もちろん、必要がなければSetterもない方がいい
    - 用意する場合はプロパティではなくメソッドの方が管理しやすい
  - Getterは値を変更される心配がないので、必要に応じて用意してもOK

# PrefabのSerializeField
## 問題点
* SerializeFieldにして外部のオブジェクトを参照していると、  
  Prefab化した時に参照が外れてしまう
  - Prefab化するなら、外部に依存するのは避けるべき
* そもそも、何でもSerializeFieldにしていると  
  依存関係が分かりづらくなりがち

## 対処法
* 参照は自身の子オブジェクト関連のみにする
  - そのオブジェクトの管理下だけで依存関係を完結させる
* Prefabを動的生成したい場合はInspector上の登録あり
  - 外部からの参照ではあるが、Prefab程度ならば依存関係が混乱する可能性は低い

# Awake/Start
## 問題点
* とりあえず`Awake()`や`Start()`で初期化してしまう
  - 初期化関数が呼ばれる順番はランダム
    - 初期化順によってバグが出たりすると発見しづらい
  - こういったオブジェクトが多いほど危険
* 不要な`Start()`や`Update()`が残っていると、
  何もないのにメソッドが呼ばれてしまう
  - パフォーマンスへの影響は少なくない

## 対処法
* 初期化に順序が必要な場合、一番最初のクラスの初期化時に  
  他のクラスの初期化処理を行うようにする
  - 初期化用のメソッドを用意し、`Start()`等は使わない
  - そもそも順序が必要＝依存関係があるということ
* 不要な`Start()`や`Update()`は早めに削除する
  - 必要になった時に追加すれば良し

# 補間関数
## 問題点
`Lerp()`等の補間関数で、指定する数値を勘違いしてしまい  
以下のような処理が生まれてしまう
```csharp
public Vector3 _targetPosition;
void Update()
{
    // targetPositionまで補間しつつ移動したい
    transform.position = Vector3.Lerp(transform.position, _targetPosition, Time.deltaTime);
}
```

* `Lerp()`等は「ある座標から別の座標までの内分点を計算する」関数
  - 3つ目の引数で指定すべきは`0.0 ~ 1.0`（最終的に1になるように）
  - `Time.deltaTime`でも確かに近づきはするが、想定される使い方ではない
    - ラグ等で`Time.deltaTime`が変わると、最終的な到着時間も変わってしまう

## 対処法
* 公式から提供されているメソッドは、ちゃんとドキュメントを読んで  
  使い方を理解する
  - 自分で書いたコードならば、説明できるように全て理解しておくべき

### `Lerp()`, `Slerp()`の場合
3つ目の引数では、基本的に最初は0・最終的に1に  
なるような数値を指定すべき

以下のようにすれば、指定した時間で確実に  
補間しつつ移動させられる。
```csharp
public Vector3 _targetPosition;

// Coroutineで実装する場合
public IEnumrator MovePosition(float moveTime)
{
    Vector3 startPosition = transform.position;

    // 毎フレームdeltaTimeを加算、指定の時間経過するまでループ
    for(float t = 0.0f; t < moveTime; t += Time.deltaTime)
    {
        // tは毎フレーム加算されるため、時間経過とともに
        // t / moveTimeは 1.0f に近づく
        transform.position = Vector3.Lerp(transform.position, _targetPosition, t / moveTime);
        yield return null;
    }

    transform.position = _targetPosition;
}
```

# Shader
## 問題点
* ピクセルシェーダーで重い処理を行ってしまう
  - `if`による条件分岐
  - 三角関数
  - `Log`や`Sqrt`など重めの数学関数

## 対処法
* 条件分岐は軽めの関数で代用する
```
// 例: 数値が負なら0、正なら1になる
// clamp で _value を 0 ~ 1に丸めて、ceilによって0よりも大きい数を1とする
ceil(clamp(_value, 0, 1))
```

* 三角関数はあらかじめテーブルを作っておくと便利
  - テクスチャに書き込んでしまう
    - (r, g, b) -> (sin, cos, tan)
* `Log`や`Sqrt`は極力使わない
  - `Sqrt`であれば、2乗してから計算を行うことで使わずに済む