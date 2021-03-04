# Infrastructure as Code(Vagrant, Ansible)

IaCの勉強会のためのVagrantとAnsibleの資料共有用のリポジトリです．

## Vagrant

後々，Vagrantの軽い説明を載せます．

## Ansible

### Ansibleについて

Ansibleは，Ansible, Inc.により開発され，2012年にリリースされた構成管理ツールである．(2015年にRed Hatに買収される)  
構成管理対象マシンに対して専用のエージェントのインストールが必要なく，記法はyamlである．  
開発言語はPythonであるため，Pythonのインストールは必要である．  

### 構成管理ツールについて

構成管理ツールとは，機器の構成をあらかじめ定義してあったファイルにより，対象の全ての機器を定義してあった構成へ変更してくれるツールである．  
これを利用することで，違う環境でも冪等性が担保された環境の構築を行うことができる．  
加えて，環境を構築するために複数台のマシンの設定やインストール等を行わなければならない場合，Ansibleを実行するだけで終わるため，工数を削減することもできる．  

## 参考文献

[*Vagrant*](https://www.vagrantup.com/)  
[*Ansible*](https://www.ansible.com/)  
[*Ansible Docs*](https://docs.ansible.com/)  
