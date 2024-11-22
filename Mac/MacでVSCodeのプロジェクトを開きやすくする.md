## `.code-workspace`をデスクトップに設置する
https://zenn.dev/yoshinani_dev/articles/76efb0ed295dcc

`.code-workspace`を作っておいてデスクトップにショートカットを置く。  
PC起動後すぐにアクセスしやすい。

## Macのopenコマンドをaliasにする
[[ターミナルからアプリを開く]]ことができるので、これをaliasに登録。

ターミナル操作をメインにしているなら、  
プロジェクトがあるディレクトリをコマンドですぐに開ける。
```bash
# 設定例（.zshrcなどに置く）
alias vsc='open -a "Visual Studio Code"'
alias vschoge='open -a "Visual Studio Code" "/path/to/project"'
```