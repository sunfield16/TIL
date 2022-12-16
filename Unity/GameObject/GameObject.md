## GameObject
Unityのゲームの基礎となるオブジェクト。

ただしGameObject単体でできることはあんまりない。  
Componentを持たせることで、機能を与えていく。

## Component
GameObjectに機能を与えるための仕組み。  
Unityにおけるゲームの振る舞いの心臓部となる。

GameObjectは **Componentのコンテナ** というようなイメージで、  
Componentを持たせることで様々な動作をさせることができる。

例えば、デフォルトで用意されているGameObjectの`Cube`をシーンに配置すると

* `Transform`（シーン上での位置や回転状態を定義するComponent）
* `MeshFilter`（3Dモデルを扱うComponent）
* `MeshRenderer`（メッシュを描画するためのComponent）
* `BoxCollider`（直方体の当たり判定を得るComponent）

を持ったGameObjectが生成される。

## Transform
GameObjectをシーン上に作成するとき、必ず持っているComponent。  

* シーン上での位置・回転・スケーリング
* オブジェクトの親子関係

といった、GameObjectがシーン上に存在するために必須の機能を持つ。