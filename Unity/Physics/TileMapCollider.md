## TileMapCollider
TileMapに配置したタイルに対して、衝突範囲を設定できる。  
TileMapにこれを付けるだけで全部のタイルに適用されるので、  
タイル1つ1つにColliderを設定する必要がない。

## タイルごとに衝突するかどうかを設定
各Tileに対して`ColliderType`を設定することで、  
タイルの種類ごとに衝突の有無を設定できる。  
`ProjectView`でTileを選択し、そこから設定可能。 

### None
衝突しない設定。  
例えば普通の道には衝突判定はいらないので、これを設定する。

### Sprite
衝突する設定。  
水面に入れないゲームの場合、水面には衝突判定が欲しいのでこれを設定する。
