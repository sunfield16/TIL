## Layer
各GameObjectをグループ分けするための機能。  
「Player」や「Enemy」といった具合で、自由に作成してそれをGameObjectに設定できる。  

## Layer Collision Matrix
`Edit` > `Project Settings...`から設定可能。  
各Layerごとに、衝突するかどうかを設定できる。

シューティングゲームでいうと、自分が撃った弾である「PlayerBullet」は「Player」には当たらないけど  
「Enemy」には当たるようにしたい…という設定を行うことが可能。
