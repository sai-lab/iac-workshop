# Ansible

## Ansibleについて

Ansibleは，Ansible, Inc.により開発され，2012年にリリースされた構成管理ツールである．(2015年にRed Hatに買収される)  
構成管理対象マシンに対して専用のエージェントのインストールが必要なく，記法はyamlである．  
開発言語はPythonであるため，Pythonのインストールは必要である．  

## 構成管理ツールについて

構成管理ツールとは，機器の構成をあらかじめ定義してあったファイルにより，対象の全ての機器を定義してあった構成へ変更してくれるツールである．  
これを利用することで，違う環境でも冪等性が担保された環境の構築を行うことができる．  
加えて，環境を構築するために複数台のマシンの設定やインストール等を行わなければならない場合，Ansibleを実行するだけで終わるため，工数を削減することもできる．  

## Playbookについて

Ansibleには，playbookというものがあり，対象マシンに対して行う動作(play)を記述するものです．  
playbookには行いたい動作(1以上)を記述します．

## 実行方法

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
$ ansible -i Hostfile -m ping
127.0.0.1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

失敗例

```bash
$ ansible -i Hostfile -m ping
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

### 使用オプション

- -i : ホストファイルを指定し，configに記載されているホストファイル以外を使用する場合，ホストファイルの場所を入れる
- --private-key : 鍵認証を行い，configに記載されている鍵ファイル以外を使用する場合，鍵ファイルの場所入れる
- -u : 使用するユーザを指定し，configに記載されているユーザ以外を使用する場合，使用ユーザを入れる．

## 構成

構成を以下に示す．

```txt
例 : 〇〇(ファイル)，〇〇/(ディレクトリ)
ansible/ (ansible用ディレクトリ)
       |- ansible.cfg (ansibleの設定ファイル)
       |- hosts (ansibleの対象を記述する)
        - playbook/ (ansibleの実行内容を記述しているファイルを置くディレクトリ)
                  |- vars/ (各種変数用ディレクトリ)
                  |      |- install.yml (インストール用変数ファイル)
                  |- install.yml (各installするタスクの指定をします)
                   - roles/ (実際に行うことを記述するファイルを置くディレクトリ)
                          |- nginx_install/ (nginxインストール用ディレクトリ)
                          |               |- files/ (使用するファイルを置くディレクトリ)
                          |               |       |- index.html (予定)
                          |               |       |- 〇.png等 (予定)
                          |               |        - nginx.conf (書き換えたnginxの設定ファイル)
                          |                - task/ (行う処理を記述するファイルを置くディレクトリ)
                          |                       - main.yml (処理を記述)
                          |- wordpress_install/ (同上)
                          |- php_install/ (同上)
                          |- mariadb_install/ (同上)
                           - timezone/ (同上)
```

## YAMLについて

構造化されたデータを表現するためのフォーマットです．

### 書き方

書き方には基本的にブロックスタイルとフロースタイルがあり，ブロックスタイルはインデントで，フロースタイルは"{}"，"[]"を用いて構造を表す．(カンマの後には空白を入れること)

#### 配列

[a, b, c]のような配列はyamlでは以下のように表せる．

```yaml
- a
- b
- c

{a, b, c}
```

#### ハッシュ

ハッシュ(key, value)はyamlでは以下のようにあらわせる．

```yaml
name: Taro
```

#### ハッシュと配列

ハッシュと配列を組み合わせて使うこともできる．

```yaml
- name: Kagawa
- name: Tokushima
- name: Ehime
- name: Kouchi

{name1: Kagawa, name2: Tokushima, name3: Ehime, name4: Kouchi}
```

#### コメント

(#)から行末までがコメントになります．

```yaml
# この行はコメント
```

#### スカラーとデータ型

配列やハッシュのような，他のデータを要素としてもつデータは「コレクション (Collection)」といいます．それ以外のデータ (数値や文字列など) は「スカラー (Scalar)」といいます．
yamlでは、以下のデータ型を自動的に判別します。

- 整数
- 浮動小数点
- 真偽値 (true, yes, false, no)
- Null値 (null, ~)
- 日付 (yyyy-mm-dd)
- タイムスタンプ (yyyy-mm-dd hh:mm:ss [+-]hh:mm)

```yaml
decimal1:  123                           # 整数 (10 進数)
decimal2:  1,234,567,890                 # 整数 (10 進数)
octal:     0644                          # 整数 (8 進数)
hexa:      0xFF                          # 整数 (16 進数)
float1:    0.05                          # 浮動小数点
bool1:     true                          # 真
bool2:     yes                           # 真
bool3:     on                            # 真
bool4:     false                         # 偽
bool5:     no                            # 偽
bool6:     off                           # 偽
null1:     ~                             # Null 値
null2:     null                          # Null 値
date:      2005-01-01                    # 日付
stamp:     2005-01-01 00:00:00 +09:00    # タイムスタンプ
str1:      'true'                        # 文字列
str2:      "2005"                        # 文字列
symbol:    :foo                          # シンボル (Syck の独自機能)
```

## 参考文献

[*Ansible*](https://www.ansible.com/)  
[*Ansible Docs*](https://docs.ansible.com/index.html)  
[*YAML*](https://magazine.rubyist.net/articles/0009/0009-YAML.html)
