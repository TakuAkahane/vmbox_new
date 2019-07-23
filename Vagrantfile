# coding: utf-8

# 仮想環境上で下記コマンドを実行した方が良い。
# sudo yum install kernel-devel
# sudo yum install gcc make

# osx で下記コマンドを実行した方が良い。
# vagrant plugin install vagrant-share
# vagrant plugin install vagrant-vbguest
#

Vagrant.configure('2') do |config|
  config.vm.provider :virtualbox do |vb|
    vb.name = 'centos7-renoperty'
    vb.customize ['modifyvm', :id, '--memory', '1024', '--cpus', '1', '--ioapic', 'on']
  end

  config.vm.box = 'centos/7'
  config.vm.hostname = 'vagrant-centos7-renoperty'
  config.vm.network :private_network, ip: '192.168.33.50'
  config.vm.network :forwarded_port, host: 3000, guest: 3000, host_ip: '127.0.0.1', id: 'HTTP'
  config.vm.network :forwarded_port, host: 9200, guest: 9200
  config.vm.network :forwarded_port, host: 5601, guest: 5601
  config.ssh.forward_agent = true
  config.ssh.insert_key = false

  config.vm.synced_folder './workspace', '/var/www/applications/workspace', type: 'nfs'
$script = <<SCRIPT
        if [ ! -e ~/workspace ]; then
          ln -s /var/www/applications/workspace ~/workspace
        fi
SCRIPT
  config.vm.provision 'shell', run: 'always', privileged: false, inline: $script
end
