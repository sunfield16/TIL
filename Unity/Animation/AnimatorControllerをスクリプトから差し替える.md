Animatorに指定するAnimatorControllerはスクリプトから差し替えることが可能。

スクリプト内で`RuntimeAnimatorController`を  
作成し、  
これを`animator.runtimeAnimatorController`に指定することで差し替えできる。
```csharp
// AnimatorControllerのファイルを生成する
RuntimeAnimatorController controller = Resources.Load<RuntimeAnimatorController>("Path/To/HogeAnimation");

_animator.runtimeAnimatorController = controller;
```

通常時のキャラクターとリザルトでのキャラクターでそれぞれAnimatorControllerを  
分けたりする場合などに有効と思われる。