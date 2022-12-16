## Hugo
`Hugo`は静的サイトジェネレーターの1つ。  
Markdown形式でコンテンツ群を用意すれば、コマンドを実行するだけで  
静的サイトを生成することが可能。

* 公式サイトに多数のテンプレートが投稿されている
  - それらを利用すれば基本的なレイアウトはノーコストで組める
* コンテンツの追加はMarkdownで作成したものを入れるだけ
* ファイル変更がリアルタイムで反映される機能あり

上記のように手軽にサイトを構築できる機能を備えており、  
主に個人ブログやポートフォリオなどで活用されている。

## 導入
MacOSであればhomebrewからダウンロード可能。
```bash
brew install hugo
```

## ワークスペースの作成
`new site`で、名前を指定してワークスペースを作成する。  
（指定した名前で自動的にディレクトリが生成される）
```bash
hugo new site [ディレクトリ名]
```

ワークスペース内は以下のようになっている。

* archetypes
* content ... Markdownなどのコンテンツを配置
* data
* layouts
* resources
* static
* themes ... テンプレートを配置する
* config.toml ... サイトの設定ファイル


## サイトのテンプレートを導入する
公式のサイトにまとめられたテンプレートを使うことで手っ取り早く始められる。

https://themes.gohugo.io/

表示サンプルを確認して、気に入ったものがあれば  
Githubのリポジトリから導入方法を確認できる。

### 導入方法例: Githubからcloneする
多くのテンプレートは`git clone`などで取得する。

作成したワークスペースに`themes`ディレクトリ（テンプレート置き場）が  
用意されているので、ここに`clone`すればOK。
```bash
cd [ワークスペース]/themes
git clone [githubリポジトリのURL]
```

## コンテンツを配置する
サイト内で見せたいコンテンツは主に`contents`に配置する。  
テンプレートで決められたディレクトリ名などのルールがあるため。  
テンプレートのREADMEなどを見ながら進めていく。


## ローカルでサイト作成・起動
配置したコンテンツで実際に生成されるサイトを確認したい場合は、  
hugoのコマンドによってサーバーを起動できる。
```bash
hugo server
```

おそらく、大体は以下のような出力がされる。
```bash
Start building sites … 
hugo v0.92.0+extended darwin/amd64 BuildDate=unknown

                   | EN  
-------------------+-----
  Pages            | 63  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     | 78  
  Processed images |  0  
  Aliases          |  2  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 116 ms
Watching for changes in /Path/To/WorkSpace/hogehoge/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Path/To/WorkSpace/hogehoge/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```
この場合は`http://localhost:1313/`にブラウザからアクセスすることで、  
生成されたサイトを表示できる。