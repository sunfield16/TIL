## Prefab
GameObjectを再利用するための機能。

ゲームにおいては、全く同じGameObjectを複製して配置することは往々にしてある。  
（敵やギミックなど）  
だが、同じオブジェクトに共通する設定をそれぞれに行ったり、設定したものを修正するときに  
複製した分すべてに適用するのは気が遠くなる。  

Prefabは、それを解消するために「オブジェクトのサンプル」を作成してそれを使い回すことができる。  
設定を修正する場合も、Prefab1つを修正するだけで配置済みの同じオブジェクトすべてに適用される。

## Prefabから生成したオブジェクトだけど一部だけ変えたい
完全に同じGameObjectならいいのだが、一部だけは異なる設定にしたい…という場合でも問題なく設定できる。  
Prefabから生成したGameObjectの設定を直接変えると、そこがPrefabから変更された部分だと分かるようになっている。  

それをPrefabのもともとの設定に戻すこともできるし、逆にそのGameObjectに行った変更をPrefab側に適用することも可能。
（Prefab側に適用すると、そのGameObjectすべてに同じ設定が入るので注意が必要）

## Prefabファイルの中身
Prefabは`.prefab`ファイルとして生成される。  
[[YAML]]形式で記述されていて、これをパースすれば  
各オブジェクトの定義や付随するコンポーネントの内容などが確認できる。

### 参考
https://blog.unity.com/ja/engine-platform/understanding-unitys-serialization-language-yaml

https://qiita.com/satanabe1@github/items/515f206659177883c7f4