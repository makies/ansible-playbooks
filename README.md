# playbooks for development

## Required

- CentOS 6.x


## Ansible

-k で ユーザ(vagrant)のパスワードを聞かれるので入力する

### vagrant 経由ではなく直接実行する場合

    $ ansible-playbook -i ansible_hosts site.yml -u vagrant -k

### タグ指定する場合（playbookの一部だけ実行したい場合）

    $ ansible-playbook -i ansible_hosts site.yml -u vagrant -k --tags タグ名


## Vagrant

Vagrant から利用する場合の設定


Vagrantfile の記述

    # HostOnlyなプライベートネットワーク
    conf.vm.network :private_network, ip: "192.168.100.1"

    # provision設定
    config.vm.provision :ansible do |ansible|
        ansible.playbook = "/path/to/makies-playbooks/site.yml"
        ansible.inventory_file = "/path/to/makies-playbooks/ansible_hosts"
    end

プライベートネットワークで指定したIPアドレスを ansible_hosts に記述する

    $ cp ansible_hosts{.sample,}

例） ansible_hosts

    [dev]
    192.168.100.1



## Futures

- LAMP環境
  - Apache2
  - PHP
    - composer
  - MySQL
  - memcached
- Node.js
  - nodebrew
  - yeomen
    - yo
    - grunt
    - bower
- 開発ツール類
    - ctags
    - vim
    - vim-enhanced
    - curl
    - git
    - subversion
    - gettext
    - make
    - automake
    - autoconf
    - man
    - unzip
    - wget
    - ntp
    - tree
 - .ssh/config
 - dotfiles init


## ToDo

- tasksに直書きしている配列物を外出しする
  - devtools のパッケージリスト
  - php関連パッケージ
  - npmのモジュールリスト
  - Apacheの設定（既存のファイルカラの差分）
  - MySQLの設定
- vim
  - :NeobundleInstall の自動化
  - vimproc の makeコマンド 自動化
- Node.js
  - パス等の設定を.bashrcに書き込む
- .ssh/config
  - no をやめたい



## Memo

- Node.js、Yeomen系のinstallがかなり時間かかるので、使わない場合はincludeしている部分をコメントアウトしてしまったほうが早い
  - roles/devtools/main.yml (nodejs.yml)
  - roles/jsapp/main.yml (yeomen.yml)
