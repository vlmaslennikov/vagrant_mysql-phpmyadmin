$mysql_install = <<~SCRIPT
  sudo ssh-keyscan github.com >> /home/vagrant/.ssh/known_hosts
  git clone git@github.com:vlmaslennikov/mysql-phpmyadmin.git 
  cd mysql-phpmyadmin
  git pull
  sudo ./mysql-phpmyadmin-install.sh $1 $2 $3
SCRIPT

$phpmyadmin_install = <<~SCRIPT
  sudo ssh-keyscan github.com >> /home/vagrant/.ssh/known_hosts
  git clone git@github.com:vlmaslennikov/mysql-phpmyadmin.git 
  cd mysql-phpmyadmin
  git pull
  sudo ./mysql-phpmyadmin-install.sh $1 $2 $3 $4 $5 
SCRIPT

Vagrant.configure(2) do |config|
  config.env.enable
  config.vm.box = ENV['VM_BOX']
  config.ssh.forward_agent = true
  
  # FIRST VM
  config.vm.define "mysql" do |mysql_config|
    mysql_config.vm.provider "virtualbox" do |vb|
      vb.name = "mysql"
    end
    mysql_config.vm.network "forwarded_port", guest: 3306, host: 3306
    mysql_config.vm.network "private_network", ip: ENV['VM_MYSQL_IP']  
    mysql_config.vm.provision "shell" do |s|
      s.inline = $mysql_install
      s.privileged = false
      s.args = "#{ENV['MYSQL_USER_PASSWORD']} #{ENV['MYSQL_ROOT_PASSWORD']} #{ENV['ALLOWED_HOST']}"  
    end
  end

  # SECOND VM
  config.vm.define "phpmyadmin" do |phpmyadmin_config|
    phpmyadmin_config.vm.provider "virtualbox" do |vb|
      vb.name = "phpmyadmin"
    end
    phpmyadmin_config.vm.network "forwarded_port", guest: 80, host: 80
    phpmyadmin_config.vm.network "private_network", ip: ENV['VM_PHPMYADMIN_IP']
    phpmyadmin_config.vm.provision "shell" do |s| 
      s.inline = $phpmyadmin_install 
      s.privileged = false
      s.args = "#{ENV['PHPMYADMIN_PASSWORD']} #{ENV['MYSQL_USER_NAME']} #{ENV['MYSQL_USER_PASSWORD']} #{ENV['MYSQL_DB_NAME']} #{ENV['MYSQL_HOST']}"
    end
  end
    
end
