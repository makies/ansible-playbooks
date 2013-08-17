# -*- mode: ruby -*-
# vi: set ft=ruby :

# dhcpでIPを取得するとansibleの対象IPが不明なのでansible実行前にifconfigして共有フォルダへゲストのIPを書き込んでおく
Vagrant.configure("2") do |config|

  config.vm.box = "cent64"
  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "~/VirtualBox VMs/box/CentOS-6.4-x86_64-ja.box"

  # プライベートIP (NFSマウントするのに必須)
  config.vm.network :private_network, :ip => "192.168.100.11"

  # コメント解除するとboot時に選択しないで済む(Mac)
  config.vm.network :public_network, :bridge => "en0: Ethernet"

  # hostname
  config.vm.hostname = "devm"

  # 共有フォルダ
  config.vm.synced_folder "./shared/", "/shared", :nfs => true

  # VirtualBoxのconfig
   config.vm.provider :virtualbox do |vb|
     # Don't boot with headless mode
     # vb.gui = true

     # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "1024"]
   end


  # 以下は初期設定用なので最初の
  # vagrant up
  # が終わったらコメントアウトするか
  # vagrant up --no-provision
  # で起動する
  # config.vm.provision :shell, :inline => $get_ip

  # config.vm.provision :ansible do |ansible|
    # ansible.playbook = "provisioning/site.yml"
    # ansible.inventory_file = "provisioning/ansible_hosts"
  # end
end
