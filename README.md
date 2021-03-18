# Infrastructure as Code Workshop configures

研究室のIaC勉強会のためのVagrantとAnsibleの資料や設定集．

## Vagrant

仮想化基盤(VirtualBox, VMware, KVM等)を設定ファイルを参照して自動で操作するソフトウェアである．
実行すると設定ファイルに書き込まれた環境のVMを簡単にコマンド一つで作成してくれる．
2012年にメジャーバージョンがリリースされ，Rubyで作成されているオープンソースのソフトウェアである．

## Ansible

Ansibleは，Ansible, Inc.により開発され，2012年にリリースされた構成管理ツールである．(2015年にRed Hatに買収される)  
構成管理対象マシンに対して専用のエージェントのインストールが必要なく，記法はyamlである．  
開発言語はPythonであるため，Pythonのインストールは必要である．  

### 構成管理ツールについて

構成管理ツールとは，機器の構成をあらかじめ定義してあったファイルにより，対象の全ての機器を定義してあった構成へ変更してくれるツールである．  
これを利用することで，違う環境でも冪等性が担保された環境の構築を行うことができる．  
加えて，環境を構築するために複数台のマシンの設定やインストール等を行わなければならない場合，Ansibleを実行するだけで終わるため，工数を削減することもできる．  

## 参考文献

[*Vagrant*](https://www.vagrantup.com/)  
[*Vagrant Docs*](https://www.vagrantup.com/docs)  
[*Ansible*](https://www.ansible.com/)  
[*Ansible Docs*](https://docs.ansible.com/)  
