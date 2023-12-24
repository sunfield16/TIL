`Shuriken`とも呼ばれている、Unity標準のパーティクル生成コンポーネント。  
非常に設定項目が多く、カスタマイズ性が高い。

ParticleSystem自身は粒子そのものである「Particle」をひたすら生成する。  
これを`Destroy()`などで削除すると、Particleもろとも急に消滅してしまうので注意が必要。  
Particleの生成を止めたいときは、`Stop()`で制御する。

必ず設定する項目の他、任意で有効・無効化できる項目もある。

## 基本設定
* Duration ... パーティクルを放出する時間の長さ（LoopingがONになっていたら関係なし）
* Looping ... ONにすると放出時間終了時にループして最初に戻る
* Prewarm ... LoopingがONの場合のみ適用。ループ再生を1回終わらせた状態から始める
* GravityModifier ... パーティクルにかかる重力（`Physics Manager`で指定した重力に依存）
* SimulationSpace ... ローカル座標で動くか、ワールド座標で動くか
  - Localにすると親オブジェクトの位置をずらした時パーティクルが一緒に動く
* SimulationSpeed ... ParticleSystemの更新速度
* DeltaTime ... `Time Scale`の値を参照するかどうか
  - UnScaledにすると`Time Scale`に関係なく動作する
* StopAction ... ParticleSystem終了時（全パーティクルが消滅するか再生終了時）に行う処理
  - LoopingがONの場合はスクリプトからの処理以外で終了しない

### `Start ~`関連
各Particleが生成されたときの設定。
固定値のほか、一定範囲のランダムな値も設定可能。

* StartLifetime ... パーティクルが放出されてから消滅するまでの時間
* StartSpeed ... パーティクルが放出される時の初速
* StartSize... パーティクルが放出される時のサイズ
* StartRotation ... パーティクルが放出される時の角度（放出される方向とは関係なし）
* StartColor ... パーティクルが放出される時の色

## `~ over LifeTime`（状態遷移）
各Particleが生成されてから消えるまでに、状態遷移をさせたい場合はこれを設定する。
固定値のほか、一定範囲でランダムにさせることも可能。

* Color over LifeTime ... 色や透明度を遷移させる
  - フェードアウトさせて消したい等の場合に使う
* Size over LifeTime ... サイズを遷移させる
  - 徐々に小さく・大きくさせたい場合に使う
* Velocity over Lifetime ... 特定方向に移動させたり速度の調整を行う
  - 特定の方向に流れたり、特定の位置を中心に漂わせたりする場合に使う
  - 徐々に加速・減速させたい場合に使う

## Emittion（放出関係の設定）
放出する数の設定や、特定タイミングでパーティクルを放出するようなイベントの  
設定を行う。

* Rate over Time ... 単位時間あたりに放出するパーティクルの数
* Rate over Distance ... 移動距離あたりに放出するパーティクルの数
  - 例えば車が走っている時などの排気ガス、埃などの演出で有効
* Bursts ... 特定時間ごとにパーティクルを放出するイベントを設定する
  - 爆発などで一気にパーティクルを出したい場合に有効

### Bursts
* Time ... 放出開始する時間（ParticleSystem開始からの秒数）
* Count ... 放出されるパーティクルの数
* Cycles ... Burstsによる放出を何回行うか
* Interval ... Burstsで放出を行う間隔（秒）
* Probablity ... パーティクルの放出を行う確率
  - 1にすると確定

## Shape
パーティクルの発生源の形状指定や、パーティクルを放出する角度などの設定を行う。  
規則的なパーティクル放出を行いたい場合にも活用できる。

形状に応じて設定項目も変わる。

### 多くの形状で共通のもの
* Radius Thickness ... パーティクルの発生源の中で、放出する領域の広さを表す（0~1）
  - 例えば形状がSphereの場合、0にすると球状の表面からしかパーティクルが出なくなる
* Arc ... 放出範囲を表す円弧の角度（360が最大）
  - 例えば形状をSphereにしてArcを180にすると、球状の左半分からしかパーティクルが出なくなる
* Mode ... パーティクル放出場所の規則性
  * Random ... 完全ランダム
  - Loop ... 時計回りのように放出場所が移動する
  - Ping-Pong ... Loopと同じだが、1週ごとに時計回りと反時計回りが切り替わる
  - Bursts Spread ... Burstsで一気に放出するときに均等に飛ぶような散らばり方をする
    - 基本はBursts用
* Randomize Direction ... 1にすると放出される方向がランダムになる
* Spherize Direction ... 1にすると発生源の中心から外側に向けて放出される
## Texture Sheet Animation
任意の画像をParticle画像に指定したい場合に設定する。  
複数の画像をランダムに使うことも可能。

## 設定方法
多くの設定項目で以下の設定方法ができる。  

* 定数
* 特定の数値の範囲でランダム
* カーブ設定（最初は数値が大きく、時間経過で小さくなるなど）
* 2つのカーブの数値の範囲でランダム

## 参考
https://docs.unity3d.com/ja/current/Manual/PartSysMainModule.html  
https://qiita.com/abcde_kind/items/e47a8f0c0f1077b314e6