# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = "2"
    vb.memory = "2048"
  end
  config.vm.provision "shell", inline: <<-SHELL
    sed -i s/archive.ubuntu.com/ftp.jaist.ac.jp/ /etc/apt/sources.list
    bash /vagrant/ubuntu_setup.sh
    cat <<EOM
After provisioning, You should login with "vagrant ssh".
Then, run below commands.

$ cd ~/redash-hands-on
$ sudo docker-compose run --rm server create_db
$ sudo docker-compose up

Finally, You can see Redash with below URL.

http://localhost:8080

Enjoy!
EOM
  SHELL
end
