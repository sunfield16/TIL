# AnimationClip
「歩き」や「ジャンプ」といったアニメーションそのもの。
3Dではモデルの動き、2Dでは画像を切り替えることによって作成する。  

# AnimationController
それぞれのAnimationClipを関連付けて、アニメーションの遷移を管理するもの。
「このパラメータを受け取ったらこのアニメーションをする」といった設定を行う。

例えばキャラクターのAnimationControllerに`Speed`というパラメータを定義して、  
`Speed`が1以上になったら「歩き」、3以上になったら「走り」に遷移する…といった感じ。

## State
AnimationControllerにおける「状態」を表す。  
「立ち状態」「歩く」「ダメージを受けた」といったアニメーションが紐づく。

## BlendTree
複数のアニメーションを、パラメータに応じて組み合わせる特殊なState。  
画面の右上に歩くような場合、「移動方向」のパラメータをもとに「右に歩く」と「上に歩く」を組み合わせる…といった感じ。

## Transition
State同士で遷移する際の動作や条件を定義する。  
「歩く」Stateから「ダメージを受ける」パラメータを受け取ると「ダメージを受けた」Stateに遷移する…というのを作成可能。

双方向に遷移するような場合はそれぞれに条件を付けられる。  
「立ち」Stateから「スピード」パラメータが一定以上になると「歩く」State、  
その状態で「スピード」パラメータが一定以下になったら「立ち」Stateに戻る等それぞれ作成が必要。

# Animator
AnimationControllerに各種パラメータを渡して、AnimationControllerにアニメーションの再生をさせるもの。  
実際にGameObjectに追加するのはこれ。

スクリプトから、「ダメージを受けた」とか「移動速度」といったパラメータをAnimatorに渡すと、  
AnimatorはAnimationControllerにそれを渡してアニメーションを遷移させる。
