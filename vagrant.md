# Vagrant
## コマンド
### 汎用
- 初期化(新規Vagrantfile作成): init [box-name] [box-url]
- 起動: up
- 停止: halt
- サスペンド: suspend
- 再起動: reload
- 再起動(provisionを再実行): reload --provision
- 再起動(指定のprovisionを再実行): reload --provision-with x,y,z
    - `:shell`だけ再実行: `vagrant reload --provision-with shell`
    - `:shell`と`:chef_solo`を再実行: `vagrant reload --provision-with shell,chef_solo`
- 削除: destroy
- 状態確認: status
- ssh接続: ssh
- 接続情報表示: ssh-config

### ボックス系
- ボックス追加: box add NAME URL
- ボックス削除: box remove NAME PROVIDER
- ボックスリスト: box list
- ボックス更新: box update
