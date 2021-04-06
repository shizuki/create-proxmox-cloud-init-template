# create-proxmox-cloud-init-template

## cloud-init対応のproxmox用テンプレートインスタンス作成用Ansibleロール

Telmate/proxmox Terraformプロバイダ使用のためのインスタンス作成用ロール

2021/04/05  
ansible 2.9.6 on ubuntu 20.04 on wslで確認

### 変数

- bashrcで定義
  - `PM_PASS`  
    Telmate/proxmox Terraformプロバイダ使用のため、予め以下の環境変数をexportしておく  
    ここに設定しておくと、あとでTerraformプロバイダが自動的にパスワードを取得してくれる

    ````sh:bashrc
    export PM_PASS=Terraformプロバイダ用ユーザが使用するパスワード
    ````

- varsで定義
  - `cloudinit.url`  
    cloud-initイメージのダウンロード元URL（ファイル名を除く）
  - `cloudinit.filename`  
    cloud-initイメージのファイル名
  - `cloudinit.checksum`  
    cloud-initイメージファイルのsha256チェックサム
  - `template.vmid`  
    テンプレートマシンのvmid
  - `template.vmname`  
    テンプレートマシンの名前（URLとして使用できるもの）
  - `template.vmmemory`  
    テンプレートマシンのメモリサイズ（MB）
  - `template.vcpucore`  
    テンプレートマシンのcpucoreの数
  - `template.vcpusockets`  
    テンプレートマシンのcpuソケットの数
  - `template.vmdiskformat`  
    テンプレートマシンのディスクイメージのインポート後のフォーマットタイプ（`qcow2`|`raw`|`vmdk`）
  - `template.vmdiskext`  
    テンプレートマシンのディスクイメージの拡張子
  - `storage`  
    テンプレートマシンを保存するproxmoxのストレージ名

### cloudinitイメージのURL

- [openstakサイト](https://docs.openstack.org/image-guide/obtain-images.html "openstack image guide")で、各OSの公式ビルドが公開されています
- Amazon Linux 2の場合、[ここ](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/amazon-linux-2-virtual-machine.html#amazon-linux-2-virtual-machine-download "Amazon Linux 2 を仮想マシンとしたオンプレミスでの実行")から「KVM」のリンクをたどった先  
  
**イメージのバージョンアップ等で変更になる場合あり**
