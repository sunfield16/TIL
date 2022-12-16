※基本的に`Vagrant init`したディレクトリで実行する必要がある。

## `init`
`Vagrant`の環境を構築したいディレクトリで下記を実行する。  
実行することでVagrantfileが生成される。

```bash
# Box名はVagrant Cloudにある名前を参照
$ vagrant init [Box名]
```

### オプション
* `--force`
  - 既にVagrantfileがあった場合でも、強制で上書きする
* `--minimal`
  - 説明コメントや記入例がない、最小限のVagrantfileを生成する

## `up`
Vagrantfileをもとに、VMを作成・起動する。  

```bash
# VM名はVagrantfileに記載してある名前を参照
# Vagrantfileがあるファイルで実行する場合は記載不要
$ vagrant up [VM名]
```

## `ssh`
起動しているVMにsshで接続する。

```bash
# VM名はVagrantfileに記載してある名前を参照
# 指定しなかった場合、「default」という名前が指定される
$ vagrant ssh [VM名]
```

### オプション
* `-c [コマンド]`, `--command [コマンド]`
  - 指定したコマンドを接続先で実行し、ssh接続を終了する
  
## `suspend`
指定したVMを一時停止する。  
完全に止めるわけではないので素早く再開でき、  
一時停止中はホストのPCのリソースを消費しない。

```bash
# VM名はVagrantfileに記載してある名前を参照
$ vagrant suspend [VM名]
```

## `resume`
`suspend`で一時停止したVMを再開させる。

```bash
# VM名はVagrantfileに記載してある名前を参照
$ vagrant resume [VM名]
```

## `halt`
指定したVMをシャットダウンする。  
完全に止めたい場合はこっち。

もしコマンドに失敗した場合、そのVMはいわゆる「強制終了」をした状態になる。

```bash
# VM名はVagrantfileに記載してある名前を参照
$ vagrant halt [VM名]
```

## `destroy`
指定したVMを削除する。  
（VMが起動中の場合は先に停止して、その後削除する）

このコマンドではBoxは削除されない。  

```bash
# VM名はVagrantfileに記載してある名前を参照
$ vagrant destroy [VM名]
```

## `status`
Vagrantが管理しているVMの状態を表示する。  
（起動・停止・一時停止など）

```bash
# VM名はVagrantfileに記載してある名前を参照
# 指定しない場合、そのディレクトリで管理している全部のVMの情報が出る
$ vagrant status [VM名]

# 下記のような感じで表示される
Current machine states:

default                   saved (virtualbox)
```
