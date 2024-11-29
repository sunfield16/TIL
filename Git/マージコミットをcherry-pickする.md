[[revertでマージコミットを取り消す]] と同じ要領。

<https://git-scm.com/docs/git-cherry-pick>  
cherry-pickで「どちらのマージ親を基準にした変更内容を持ってくるのか」  
を決めるイメージ。  
revertの場合は「どちらのマージ親の状態に戻すのか」を決めるイメージ。
```
-m <parent-number>
--mainline <parent-number>
Usually you cannot cherry-pick a merge because you do not know which side of the merge should be considered the mainline.
This option specifies the parent number (starting from 1) of the mainline and allows cherry-pick to replay the change relative to the specified parent.

---

-m <親番号>
--mainline <親番号>
通常、マージのどちら側をメインラインと見なすべきかわからないため、チェリーピックでマージすることはできません。このオプションは、メインラインの親番号 (1 から始まる) を指定し、チェリーピックで指定された親を基準とした変更を再生できるようにします。
```