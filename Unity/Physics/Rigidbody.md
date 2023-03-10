## Rigidbody
ゲームには欠かせない「物理に従う物体」を扱う。  
これを設定したGameObjectは物理法則の影響を受け、  
重力で下に落ちたり何かに力を受けて押されたりといった動きを表現できる。

## BodyType
### Dynamic
物理に従って動く状態。
動く想定の物体はこれを設定する。

### Static
物理の一切合切を受け付けない、静的な状態。  
動かない物体にはこれを設定しておくと、動く心配がないしパフォーマンス的にも有効。

## Mass
物体の重さ。これを大きくすると、外部から力を受けても動きにくくなる。

## GravityScale
重力の強さ。これが強いほど受ける重力が強く、より速く落ちていく。  
0にすると落ちない。

## Constraints
物体を固定するための設定。  
BodyTypeとは別に、一定方向にだけ動かない物体を表現したい場合はこれ。

### Freeze Position
外部から力を受けても、指定の軸方向に移動しない設定ができる。  

### Freeze Rotation
外部から力を受けても、指定の軸方向に回転しない設定ができる。  
2DはZ軸のみ対応。

## Interpolate
フレーム単位での更新時に補間を適用する。  
Rigidbodyの動きがぎこちない時に設定すると改善されるかもしれない。

### Interpolate
前フレームの`Transform`に基づいた補間を行う。

### Extrapolate
次のフレームの`Transform`を予測して補間を行う。

## Collision Detection
衝突検知の方法を指定する。  
高速で動くオブジェクトが壁などの判定をすり抜けてしまう場合は、  
この設定を調整すると改善されるかもしれない。

`Rigidbody2D`には`Discrete`と`Continuous`だけしかない。

### Discrete
離散型の衝突検知を使用する。基本的にはこれを使う。

### Continuous
場合によって連続型の衝突検知を使用する。
「高速で動くオブジェクトがぶつかってくるもの」にはこれを指定する。
物理演算のパフォーマンス上あまり良くないので、  
問題が出ない限りは`Discrete`の方が良い。

衝突する相手によって以下の検知方法を使い分ける。
* 動的なコライダー (リジッドボディあり) ...  離散型の衝突検知
* 静的メッシュコライダー (リジッドボディなし) ...  連続型の衝突検知

### Continuous Dynamic
これも連続型の衝突検知を使用するが、  
「高速で動くオブジェクト」にはこっちを指定する。

衝突する相手によって以下の検知方法を使い分ける。
* `Continuous`や`Continuous Dynamic`を指定したオブジェクト ... 連続型の衝突検知
* 静的メッシュコライダー (リジッドボディなし) ... 連続型の衝突検知
* その他 ... 離散型の衝突検知