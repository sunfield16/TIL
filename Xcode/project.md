## Target
Xcodeのプロジェクトに必ず1つ以上存在する、ひとまとまりのビルド設定。  
ビルドする際にはSchemeに紐づいたTargetの設定が使われる。

基本的には「iOS」や「OSX」といったビルド成果物の単位ごとに  
Targetを分けることになる。

## Scheme
`Run`や`Archive`といった各ビルド方法ごとに、どのTargetを使うかや  
Debug・Releaseビルドのどちらを行うか等の設定をまとめたもの。

Xcode上ではこのSchemeを選択してビルドを行うことになる。

## Project(xcodeproj)
ProjectはXcodeで管理できるプロジェクトを表し、  
複数のTargetをグループ化するもの。

Projectにもビルド設定を行うことができる。  
全Targetで共通するベース設定をProjectで行うイメージ。

## SubProject
Projectには子として別のProjectを含めることができる。  
これがSubProjectであり、SubProject単体で開くことも可能。

親Projectをビルドする時も依存関係としてSubProjectがビルドされる。

例えばcocos2d-xでの開発では、メインになるProjectに  
cocos2dがSubProjectとして追加される。

## Workspace(xcworkspace)
複数のProjectを同じ階層でグループ化したもの。  
SubProjectは親子関係だが、こちらはProject同士を同列で扱う。

例えばCocoaPodsを導入すると、CocoaPods用のProjectが1つ作成されて  
もとのProjectとグループ化されたWorkspaceが出来上がる。