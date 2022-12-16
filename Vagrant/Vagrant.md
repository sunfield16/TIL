## Vagrant
`Virtual Box`などの「仮想マシン(VM)」を動かすソフトを扱いやすくするためのラッパーツール。  
VMを使った複雑な環境構築をサポートする。

VMの構成や構築手順をファイルに記述する仕組みで、様々な利点がある。 
* 設定ファイルがそのまま「環境構築資料」になる
  - 実際の構築手順もVagrantのコマンド操作だけでいいので簡単
* 複数人で開発する際も設定ファイルを共有するだけで済むので、全員で開発環境を合わせやすい
* 設定はテキストファイルなので、gitでの管理がしやすい

## Vagrantfile
VMの構成情報を記述したファイル。中身は`ruby`で記述する。  
Vagrantはこれに書いた情報をもとにVMを構築してくれる。  

記述する情報の例として下記が挙げられる。  
* VMのマシン名
* 保有メモリ
* ディスク容量
* 構築時に実行するコマンド
  - ユーザーやグループの作成を行える
  - その他、VMにインストールしておきたいソフトがある場合は、ここでコマンドを実行する

## Box
Vagrantで扱う、VMのベースになる構築情報。  
VagrantfileではまずBoxをベースにして、そこから必要な各種設定を追加していくことになる。

Boxは[Vagrant Cloud](https://app.vagrantup.com/boxes/search)にまとまっている。

#  Vagrant始め方
例として、`Ubuntu`を起動する想定で始め方を記載。

## ダウンロード
[公式サイト](https://www.vagrantup.com/)からダウンロード可能。  
また、`VirtualBox`などのVM構築ソフトは別途ダウンロードが必要。

インストールが完了したら、コンソールで下記を実行することで  
正常にインストールされていることが確認できる。

```bash
# バージョン確認コマンド
$ vagrant -v
Vagrant 2.2.14
```

## デフォルトの設定ファイルを作成
任意のディレクトリを作成して、下記を実行する。
```bash
# --minimalを付けると、コメントや記入例が省略された「最小限」のVagrantfileが生成される
# 「ubuntu/trusty64」でVagrant CloudにあるBoxを指定している
$ vagrant init --minimal ubuntu/trusty64
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

現在のディレクトリに`Vagrantfile`というファイルが作成される。  
これがVMの設定ファイルになる。

## 起動・ログイン・停止
もう起動することは可能。  
起動する際は、Vagrantfileがあるディレクトリで下記を実行する。
```bash
$ vagrant up
```

問題なく起動していれば、下記コマンドでsshログインが可能。
```bash
$ vagrant ssh
```

停止する場合は下記を行う。
```bash
$ vagrant halt
```
