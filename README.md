# Infrastructure as Code(Vagrant, Ansible)

IaCの勉強会のためのVagrantとAnsibleの資料共有用のリポジトリです．

## Vagrant

後々，Vagrantの軽い説明を載せます．

## Ansible

### Ansibleについて

Ansibleは，Ansible, Inc.により開発され，2012年にリリースされた構成管理ツールである．(2015年にRedHatに買収される)  
構成管理対象マシンに対して専用のエージェントのインストールが必要なく，記法はyamlである．  
開発言語はPythonであるため，Pythonのインストールは必要である．  

### 構成管理ツールについて

構成管理ツールとは，機器の構成をあらかじめ定義してあったファイルにより，対象の全ての機器を定義してあった構成へ変更してくれるツールである．  
これを利用することで，違う環境でも冪等性が担保された環境の構築を行うことができる．  
加えて，環境を構築するために複数台のマシンの設定やインストール等を行わなければならない場合，Ansibleを実行するだけで終わるため，工数を削減することもできる．  

### Playbookについて

Ansibleには，playbookというものがあり，対象マシンに対して行う動作(play)を記述するものです．  
playbookには行いたい動作(1以上)を記述します．

### 実行方法

以下にAnsibleの実行方法を示す．
自分で作成したplaybookを使う場合は，ansible-playbookコマンドを用いる．
形式

```bash
ansible-playbook [options] playbookfile
```

使用例

```bash
ansible-playbook -i Hostfile playbookfile --private-key=keyfiles -u ansible
```

次に，接続の確認を行う方法を示す．
成功例

```bash
$ ansible 127.0.0.1 -m ping
127.0.0.1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

失敗例

```bash
$ ansible 127.0.0.2 -m ping
127.0.0.2 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '127.0.0.2' (ECDSA) to the list of known hosts.\r\nhata@127.0.0.2: Permission denied (publickey).\r\n",
    "unreachable": true
}
```

ansibleコマンドはデフォルトのモジュールを1回行う場合等に用いる．
形式

```bash
ansible [pattern] -m [module] -a "[module options]"
```

#### 使用オプション

- -i : ホストファイルを指定し，configに記載されているホストファイル以外を使用する場合，ホストファイルの場所を入れる
- --private-key : 鍵認証を行い，configに記載されている鍵ファイル以外を使用する場合，鍵ファイルの場所入れる
- -u : 使用するユーザを指定し，configに記載されているユーザ以外を使用する場合，使用ユーザを入れる．

### YAMLについて

構造化されたデータを表現するためのフォーマットです．

#### 書き方

書き方には基本的にブロックスタイルとフロースタイルがあり，ブロックスタイルはインデントで，フロースタイルは"{}"，"[]"を用いて構造を表す．(カンマの後には空白を入れること)

##### 配列

[a, b, c]のような配列はyamlでは以下のように表せる．

```yaml
- a
- b
- c

{a, b, c}
```

##### ハッシュ

ハッシュ(key, value)はyamlでは以下のようにあらわせる．

```yaml
name: Taro
```

##### ハッシュと配列

ハッシュと配列を組み合わせて使うこともできる．

```yaml
- name: Kagawa
- name: Tokushima
- name: Ehime
- name: Kouchi
```
