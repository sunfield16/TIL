## ParticleSystem
ゲームにおける煙などの粒子が舞う演出「パーティクル」を、細かく設定して作成できるGameObject。  
自由度が非常に高い。

ParticleSystem自身は粒子そのものである「Particle」をひたすら生成する。  
これを`Destroy()`などで削除すると、Particleもろとも急に消滅してしまうので注意が必要。  
Particleの生成を止めたいときは、`Stop()`で制御する。

必ず設定する項目の他、任意で有効・無効化できる項目もある。

## 設定項目(Start ~~~)
各Particleが生成されたときの設定。
固定値のほか、一定範囲のランダムな値も設定可能。

### Start LifeTime
生成されてから消えるまでの時間を設定する。  

### Start Speed
生成されたときの速度を設定する。

### Start Size
生成されたときのサイズを設定する。

## Simulation Space
生成されたParticleがどこを基準に移動するかを設定する。  
`Local`だと、ParticleSystemの親GameObjectの位置に合わせて移動する。  
`World`だと親GameObjectが移動しても位置が変わらない。

例えば「車の排気煙」は車と一緒に移動してほしくないので、`World`が望ましい…といった感じ。

## 設定項目(~~~ over LifeTime)
各Particleが生成されてから消えるまでに、状態遷移をさせたい場合はこれを設定する。
固定値のほか、一定範囲でランダムにさせることも可能。

### Color over LifeTime
色や透明度を遷移させる。  
フェードアウトさせて消したい等の場合はこれ。

### Size over LifeTime
サイズを遷移させる。  
徐々に小さく・大きくさせたい場合はこれ。

## Texture Sheet Animation
任意の画像をParticle画像に指定したい場合に設定する。  
複数の画像をランダムに使うことも可能。
