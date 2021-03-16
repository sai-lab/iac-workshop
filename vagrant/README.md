# Vagrant

## Vagrantについて

仮想化基盤(VirtualBox, VMware, kvm等)を設定ファイルを参照して自動で操作するソフトウェアである．
実行すると設定ファイルに書き込まれた環境のVMを簡単にコマンド一つで作成してくれる．
2012年にメジャーバージョンがリリースされ，Rubyで作成されているオープンソースのソフトウェアである．

### 実行方法

Vagrantfileのダウンロード

```bash
vagrant init box名
```

仮想マシンの作成(VirtualBoxの場合)

```bash
vagrant up --provider=virtualbox
```

仮想マシンへのログイン

```bash
ssh -p ポート番号 ユーザ名@localhost
```

Vagrantfileが存在するディレクトリにて

```bash
vagrant ssh
```

仮想マシンの起動

```bash
vagrant up
```

仮想マシンの停止

```bash
vagrant halt
```

仮想マシンの保留

```bash
vagrant suspend
```

仮想マシンの保留からの起動

```bash
vagrant resume
```

仮想マシンの再起動

```bash
vagrant reload
```

仮想マシンの削除

```bash
vagrant destroy
```

### Vagrantfileについて

VagrantfileはRubyの記法に従って書く，VMの構成やネットワーク等の設定について書く．
以下に基本的な内容について書く．

- vm.box : string型，使用するbox名を記述．
- vm.box_check_update : boolean型，起動時にboxの更新があるかを確認，ある場合は通知する．
- vm.network : 使用するネットワークについて書く．
  - private_network : 使用するプライベートIPについて書く．DHCPにて動的に割り当てる際には記述の必要はなく次の行に動的に割り当てる方法を記述する．(type: "dhcp")ip:"192.168.xxx.yyy"
  - public_network : 使用するパブリックIPについて書く．前述と同様．DHCPにて動的に割り当てる際には，ipの記述の必要はない．
  - forwarded_port : フォワードするポート番号を記述する．guestの後にVMのポート番号を，hostの後にフォワードするポート番号を書く．IDの後に，分類の名前を書くこともできる．guest: 80, host: 8080, id: "http"
- vm.synced_folder : 共有するディレクトリの設定を行います．ホスト上のディレクトリ，VMのディレクトリの順番に記述します．
  - create : boolean型，ホスト上にディレクトリが無い場合作成します．
  - group, owner : string型，ディレクトリのグループとオーナーを指定します．
- vm.provider : 仮想化基盤での設定を記述します．
  - name : string型，VMの名前を記述する．指定しない場合，デフォルトはVMを作成したタイムスタンプの値になります．
  - gui : boolean型，GUIの有無を指定します．デフォルトはtrueになっています．
  - cpus : int型，割り当てるCPUの個数を記述します．
  - memory : string型，割り当てるメモリ量(MB)を記述します．

## 参考文献

[*Vagrant*](https://www.vagrantup.com/)  
[*Vagrant Docs*](https://www.vagrantup.com/docs)
