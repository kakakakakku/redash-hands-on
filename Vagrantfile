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
    apt-get update
    apt-get upgrade -y
    apt-get install -y language-pack-ja \
      apt-transport-https \
      ca-certificates \
      curl \
      software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
    apt-get update
    apt-get install -y docker-ce
    curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    systemctl start docker
  SHELL
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    git clone https://github.com/kakakakakku/redash-hands-on.git
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
