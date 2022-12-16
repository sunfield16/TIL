## SpineWebPlayer
SpineWebPlayerはSpine公式から提供されているアニメーションビューアー。  
`.js`と`.css`の形で配布されていて、簡単なJavascriptの記述だけで自分のWebサイトに配置することが可能。

読み込まれたスケルトンデータに含まれるアニメーションを任意で再生できるほか、
デバッグ機能としてボーンやメッシュの表示などもできる。  

ただしスケルトンはjsonに限られ、  
バイナリで出力されたもの(.skel)は表示できない。

## 機能
* 任意のアニメーション再生
* 再生速度の変更
* 設定されているボーン・メッシュ等の表示
* 背景の変更
* 各種プレイヤー機能の表示・非表示設定
  - 非表示にすると単純にデフォルトで設定されたアニメーションを再生するだけになる

## 実装方法
参考：公式サイト  
http://ja.esotericsoftware.com/spine-player

### Spineリポジトリをダウンロード
[SpineのGitHub](https://github.com/EsotericSoftware/spine-runtimes)からリポジトリをclone、またはzipでダウンロードする。

### WebPlayer用ファイルのダウンロード・配置
[spine-tsのページ](https://github.com/EsotericSoftware/spine-runtimes/tree/3.8/spine-ts)を参考に、  
WebPlayer用の各種ファイルを自分のWebサイトのディレクトリに配置する

```
spine-ts/build/spine-player.js
spine-ts/player/css/spine-player.css
```

### WebサイトにWebPlayer用のコンテナを作成
ソース上で配置したい場所にコンテナを作成する。

```html
<!-- WebPlayerで指定するのでidが必要 -->
<!-- スタイルは自由 -->
<div id="player-container" style="width: 640px; height: 480px;"></div>
```

### WebPlayerを生成
再生したいSpineファイルのパスを指定する。  
ブラウザによってはURLを絶対パス指定にしないと読み込めない場合があるので注意が必要。
```html
<!-- 1つ目の引数にはコンテナのidを指定する -->
<script>
new spine.SpinePlayer("player-container", {
      jsonUrl: "/path/to/file.json",
      atlasUrl: "/path/to/file.atlas",
});
</script>
```

これにより、指定したコンテナにWebPlayerが表示される。

### オプション指定
生成時に様々なオプションを指定可能。


オプション     | 内容
-------------|----------
animation    | デフォルトで再生されるアニメーション
showControls | デバッグ用メニューを表示/非表示

```html
<!-- 設定例 -->
<script>
new spine.SpinePlayer("player-container", {
      jsonUrl: "/path/to/file.json",
      atlasUrl: "/path/to/file.atlas",
      animation: "walk"
      showControls: false
});
</script>
```